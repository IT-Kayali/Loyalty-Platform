# Architekturübersicht

## Verbindlicher technischer Rahmen

Die Plattform wird als **modularer Multi-Tenant-Monolith** aufgebaut.

```text
Browser / WordPress
        |
        v
Reverse Proxy
   |         |
   v         v
Next.js     NestJS API
               |
      +--------+--------+
      |        |        |
 PostgreSQL   Redis   Object Storage (später)
               |
             BullMQ
               |
             Worker
```

## Verantwortlichkeiten

### WordPress

Später sichtbare Kundenoberfläche für Marketing, Account, Checkout, Aboverwaltung und Einstieg in die SaaS. Händler werden nicht auf eine separate Server-/Admin-Domain weitergeleitet.

### Next.js / React

Komplexe SaaS-Oberflächen wie Händlerverwaltung, POS, Data Grids, Card Builder, Live Preview, Analytics und QR-Scanner.

### NestJS

Autoritative Sicherheits- und Business-Schicht. Tenant, Permissions, Plan/Entitlements und Loyalty-Regeln werden ausschließlich serverseitig entschieden.

### PostgreSQL

Source of Truth für fachliche Daten. Tenant-gebundene Tabellen erhalten `tenant_id`; PostgreSQL Row Level Security wird als Defense-in-Depth eingesetzt.

### Redis / BullMQ

Cache und Background Jobs. Redis ist niemals alleinige Source of Truth.

## Sicherheitsgrenzen

- Nur der Betreiber erhält Infrastrukturzugriff.
- Händler, Mitarbeiter und Endkunden verwenden ausschließlich HTTPS-Anwendung/API.
- PostgreSQL, Redis, Worker, Docker API und interne Monitoring-Ports werden nicht öffentlich exponiert.
- Cross-Tenant-Zugriffe müssen technisch und durch Tests verhindert werden.

## Loyalty-Grundprinzip

Jeder Endkunde besitzt **pro Händler eine eigene Loyalty-Karte**. Eine Händlerkarte kann mehrere Programme enthalten: Punkte, mehrere Stempelkarten, Levels, Rewards und Gutscheine.

## Datenintegrität

- Punkte und Stempel werden über immutable Ledger geführt.
- Materialisierte Salden dienen schnellen Reads.
- Refunds erzeugen Reversal-Einträge; historische Ledger-Einträge werden nicht überschrieben.
- Externe Events und kritische Writes sind idempotent.
- Voucher Redemption muss atomar und Double-Spend-sicher sein.

## Billing

Billing ist ein austauschbares Integrationsmodul. Während der ersten Entwicklungsphase besteht **keine direkte Stripe-Abhängigkeit**. Der SaaS-Kern arbeitet mit eigener Subscription-/Entitlement-Projektion und einer provider-neutralen Provisioning-Schnittstelle.
