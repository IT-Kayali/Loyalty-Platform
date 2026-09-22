# Loyalty Platform

Multi-Tenant Loyalty & Rewards SaaS für lokale, Online- und Hybrid-Händler.

> **Arbeitsregel:** Dieses Projekt wird ausschließlich im Repository **IT-Kayali/Loyalty-Platform** entwickelt. Änderungen für dieses SaaS-Projekt dürfen nicht in andere Repositories geschrieben werden.

## Produktziel

Die Loyalty Platform soll Händlern ermöglichen, ein eigenes digitales Treueprogramm unter ihrer eigenen Marke anzubieten, ohne eine eigene Loyalty-Infrastruktur entwickeln zu müssen.

Ein Händler kann seine Kunden lokal, online oder hybrid über **ein gemeinsames Loyalty-Konto pro Händler** bedienen. Endkunden besitzen **keine globale händlerübergreifende Punktekarte**, sondern für jedes Unternehmen eine eigene Händler-Loyalty-Karte.

Langfristige Kernziele:

- einfache Einrichtung für kleine und mittlere Händler
- Punkteprogramme und digitale Stempelkarten
- Rewards und Gutscheine
- QR-basierte Identifikation
- mobile POS-/Mitarbeiteroberfläche
- Customer Portal für Endkunden
- später Apple Wallet und Google Wallet
- später WooCommerce, Shopify, weitere POS-/Kassensysteme und Public API
- klare Multi-Tenant-Trennung und hohe Nachvollziehbarkeit
- SaaS-Tarife, Limits und Feature-Entitlements
- DSGVO-konforme Prozesse, Audit und sichere Datenhaltung
- modularer Ausbau ohne bestehende Funktionen unbeabsichtigt zu beschädigen

## Zielgruppen

Die Plattform richtet sich insbesondere an Cafés, Bäckereien, Restaurants, Friseure, Barbershops, Beauty- und Kosmetikstudios, Einzelhandel, Dienstleister, lokale Händler mit mehreren Filialen, Online-Shops und Hybrid-Händler.

## Benutzerrollen

### Platform Super Admin
Verwaltet Tenants, Trials, Pläne, Limits, Feature Flags, Templates, Integrationen, Systemstatus, Jobs, Queues, Audit Logs und Supportzugriffe.

### Tenant Owner
Verwaltet Unternehmen, Branding, Filialen, Mitarbeiter, Rollen, Kunden, Loyalty-Programme, Stempelkarten, Rewards, Gutscheine, Analytics, Integrationen, API-Zugänge und Planstatus.

### Manager
Erhält konfigurierbare Teilrechte und optional einen Filial-Scope.

### Mitarbeiter
Arbeitet hauptsächlich im POS-Modus: Kunde suchen oder scannen, Kauf erfassen, Punkte oder Stempel vergeben und Rewards bzw. Gutscheine einlösen.

### Marketing
Kann später Kampagnen, Segmente, Rewards, Aktionen und Analytics verwalten.

### Endkunde
Sieht nur seine eigenen Händlerkarten und Daten: QR-Code, Punktestand, Stempelkarten, Rewards, Gutscheine, Level, Aktivitäten und Consent-Einstellungen.

## Zentrales Loyalty-Modell

~~~text
Global Identity
   ↓
Tenant Customer Profile
   ↓
Merchant Loyalty Card
   ├─ Points Program
   ├─ Stamp Card A
   ├─ Stamp Card B
   ├─ Level Program
   ├─ Rewards
   ├─ Vouchers
   └─ Activity / Ledgers
~~~

Eine Person kann Kunde bei mehreren Händlern sein. Jeder Händler sieht ausschließlich seine eigenen Kundendaten und Loyalty-Daten.

## Händler-Loyalty-Karte

Pro Händler erhält der Kunde eine eigene digitale Loyalty-Karte. Diese kann enthalten:

- Händlerlogo und Branding
- Kundenname / Mitglieds-ID
- QR-Code
- Punktestand
- mehrere Stempelkarten
- Level
- verfügbare Rewards
- Gutscheine
- Aktivitätshistorie
- später Apple-Wallet- und Google-Wallet-Integration

Die Loyalty-Karte ist der Container der Kundenbeziehung zum jeweiligen Händler.

## Punkte

Punkte werden nicht als frei manipulierbarer Kontostand behandelt. Änderungen laufen über ein nachvollziehbares Ledger.

~~~text
Aktion
→ Validierung
→ Regelberechnung
→ Ledger-Eintrag
→ materialisierter Kontostand
→ Event / Audit
~~~

Ziele:

- vollständige Historie
- Refunds/Reversals ohne Überschreiben alter Transaktionen
- Schutz vor Doppelbuchungen
- nachvollziehbare manuelle Korrekturen
- spätere Punkteverfallsregeln
- Debt Balance bei Rückerstattung nach bereits eingelösten Rewards

Für das MVP sollen Punkte grundsätzlich ganzzahlig behandelt werden, sofern später keine andere fachliche Entscheidung getroffen wird.

## Digitale Stempelkarten

Ein Händler kann mehrere Stempelkarten gleichzeitig anbieten.

Geplant sind:

- Template Gallery
- Händlerkopien von Templates
- visueller Card Builder
- Live Preview
- frei definierbare Stempelanzahl
- Reward nach Abschluss
- Regeln nach Einkauf, Umsatz, Produkt, Kategorie oder manuell
- Filial-/Channel-Scope
- Limits
- wiederholbare Zyklen
- vollständige Stamp-Historie

## Rewards und Gutscheine

Geplante Reward-Typen:

- Gutschein
- Rabatt
- Gratisprodukt
- Gratisleistung
- Bonuspunkte
- individuelle Belohnung

Ein ausgegebener Customer Reward erhält einen Snapshot seiner Bedingungen. Spätere Änderungen am Reward dürfen bestehende Kundenansprüche nicht rückwirkend verändern.

Gutscheine benötigen eindeutigen Code/QR, Status, Gültigkeit, Händler-/Filial-Scope, Einlösungshistorie, Double-Spend-Schutz und sichere Reversal-Logik.

## POS / Mitarbeiterbetrieb

Der POS wird scan-first aufgebaut.

~~~text
Kunden-QR scannen
→ Kunde wird geladen
→ Betrag / Aktion eingeben
→ Punkte-/Stempelvorschau
→ bestätigen
→ Ledger schreiben
→ Reward prüfen
→ Erfolg
~~~

Die Oberfläche muss auf Smartphone, Tablet und Desktop funktionieren. Mitarbeiter erhalten keinen unnötigen Adminzugriff.

## Customer Portal

Der Endkunde benötigt für das MVP keine native App.

Das Customer Portal wird mobile-first entwickelt und zeigt:

- Meine Karten
- Händlerkarte
- QR-Code
- Punkte
- Stempelkarten
- Rewards
- Gutscheine
- Aktivitäten
- Profil
- Datenschutz / Consent

Das Portal bleibt die vollständige Kundenansicht. Wallets sind später eine zusätzliche Projektion.

## Apple Wallet und Google Wallet

Wallet-Unterstützung kommt nach stabilem Core.

Ziele:

- Händlerlogo und Branding
- QR-/Barcode
- Mitgliedsinformationen
- **aktueller Punktestand direkt im Wallet**
- optional Level- oder Reward-Information
- serverseitige Aktualisierung nach Loyalty-Transaktionen

Wichtig: Das SaaS-Backend bleibt immer die Source of Truth. Apple Wallet und Google Wallet sind nur Projektionen des aktuellen Backend-Status.

## Online, lokal und hybrid

Unterstützte Channels:

- POS / lokal
- Web
- WooCommerce
- Shopify
- Public API
- manuell

Hybrid bedeutet nicht zwei Konten. Ein Kunde sammelt beim selben Händler online und lokal auf derselben Händler-Loyalty-Karte, sofern die Programmregeln dies erlauben.

## WordPress-Strategie

WordPress wird **nicht** zum fachlichen Kern der Loyalty-Plattform.

| Bereich | Verantwortung |
| --- | --- |
| WordPress | Marketing, Preise, Account-Einstieg, später Checkout/Subscription/Billing |
| Next.js | Merchant UI, POS, Customer UI und komplexe Frontend-Funktionen |
| NestJS | autoritative Business- und Security-API |
| PostgreSQL | Source of Truth |
| Redis/BullMQ | Cache und Background Jobs |

Die SaaS wird zuerst unabhängig und sauber aufgebaut. Die WordPress-Anbindung erfolgt anschließend über definierte APIs und Contracts.

Der Händler soll später sichtbar auf der zentralen Webseite bleiben, z. B. unter /mein-konto/saas/. Es soll keine sichtbare Weiterleitung auf eine interne Server- oder Admin-Domain geben.

## Billing-Strategie

**Keine direkte Stripe-Abhängigkeit im Loyalty-Kern.**

Billing und Subscription werden provider-neutral aufgebaut.

~~~text
Billing Provider / WordPress
        ↓
Billing Adapter
        ↓
Subscription / Entitlement Service
        ↓
Tenant + Plan + Features + Limits
~~~

Damit kann später Stripe, ein WordPress-Subscription-System oder ein anderer Anbieter angebunden werden, ohne die Loyalty-Domain umzubauen.

Während der Entwicklung können Test-Tenants und Test-Pläne intern provisioniert werden.

## Multi-Tenancy

Die Plattform ist eine echte Multi-Tenant-SaaS.

Grundprinzipien:

- Shared PostgreSQL zum Start
- tenant_id auf tenantgebundenen Daten
- Row Level Security als Defense-in-Depth
- Tenant Context serverseitig
- keine Tenant-Autorisierung anhand von Browserdaten
- Tenant-Isolation für API, DB, Jobs, Cache, Files, Exporte, Integrationen und Analytics
- Cross-Tenant-Tests für zentrale Ressourcen

Später können Enterprise-Tenants bei Bedarf auf dedizierte Datenbanken verschoben werden.

## Rollen und Sicherheit

Jeder Request folgt grundsätzlich:

~~~text
Authentication
→ Tenant Context
→ Tenant Membership
→ Permission Check
→ Location Scope
→ DB / RLS Context
→ Domain Operation
→ Audit / Response
~~~

Weitere Sicherheitsziele:

- sichere Sessions
- Refresh Token Rotation
- MFA für Super Admin
- MFA-Empfehlung für Tenant Owner
- Argon2id für Passwörter
- Rate Limits
- CSRF-/XSS-/SQLi-Schutz
- sichere QR-Identifier ohne interne DB-IDs
- API Keys nur als Hash
- Secrets nicht im Repository
- Audit für kritische Aktionen
- PostgreSQL, Redis, Worker und Docker API niemals öffentlich

## Technische Zielarchitektur

- **Frontend:** Next.js / React / TypeScript
- **Backend/API:** NestJS / TypeScript
- **Datenbank:** PostgreSQL
- **ORM:** Prisma; kritische Vorgänge mit expliziten DB-Transaktionen und Locks
- **Cache & Jobs:** Redis + BullMQ
- **Deployment:** Docker / Docker Compose
- **Reverse Proxy:** Caddy oder Traefik
- **API-Dokumentation:** OpenAPI / Swagger
- **UI-Basis:** Radix UI Primitives + eigenes Design System
- **Storage:** später S3-kompatibler Object Storage
- **CI/CD:** GitHub Actions
- **Monitoring:** Prometheus + Grafana
- **Logs:** Loki
- **Error Tracking:** Sentry oder GlitchTip

## Architekturprinzip

Start als **modularer Monolith**, nicht als Microservice-Landschaft.

Gründe: schnellere MVP-Entwicklung, einfachere Transaktionen, weniger Betriebsaufwand, klare Domain-Grenzen und trotzdem spätere Trennbarkeit einzelner Komponenten.

## Repository-Struktur

~~~text
Loyalty-Platform/
├─ apps/
│  ├─ merchant-web/
│  ├─ customer-web/
│  ├─ admin-web/
│  ├─ api/
│  └─ worker/
├─ packages/
│  ├─ ui/
│  ├─ design-tokens/
│  ├─ api-client/
│  ├─ contracts/
│  ├─ validation/
│  ├─ auth/
│  ├─ i18n/
│  ├─ observability/
│  └─ config/
├─ domains/
│  ├─ identity/
│  ├─ tenancy/
│  ├─ iam/
│  ├─ customers/
│  ├─ locations/
│  ├─ loyalty/
│  ├─ stamp-cards/
│  ├─ rewards/
│  ├─ vouchers/
│  ├─ orders/
│  ├─ integrations/
│  ├─ wallet/
│  ├─ campaigns/
│  ├─ notifications/
│  ├─ analytics/
│  ├─ billing/
│  └─ audit/
├─ infrastructure/
├─ docs/
└─ tooling/
~~~

## Entwicklungs-Roadmap

### R0 – Foundation
Repository, Monorepo, Development/Staging, Docker, PostgreSQL, Redis, Worker, Config/Secrets, Logging, Healthchecks und GitHub Actions.

### R1 – Identity & Tenancy
Login, Sessions, Tenant Context, RLS, RBAC, Permissions, Location Scope und Audit.

**Abnahme:** Zwei Test-Tenants können sich anmelden und niemals gegenseitig ihre Daten sehen.

### R2 – Provider-neutrales Provisioning
Test-Tenant erstellen, Owner erstellen, Plan zuweisen, Features/Limits verwalten, Entitlement-Grundlage; WordPress/Billing-Adapter später.

### R3 – Merchant Core
Unternehmen, Branding, Filialen, Mitarbeiter, Rollen, Kunden, Customer Tenant Profiles, Händler-Loyalty-Karte und QR-Identifier.

### R4 – Loyalty Core
Punkteprogramme, Immutable Points Ledger, Balances, QR und Refund-/Reversal-Grundlage.

### R5 – Stamp Cards
Globale Templates, Gallery, Card Builder, Live Preview, Rules, Limits, Stamp Cycles und Immutable Stamp Ledger.

### R6 – Rewards & Vouchers
Reward Definitions, Customer Rewards, Snapshots, Voucher Issuance, Redemption und Double-Spend-Schutz.

### R7 – POS
QR Scanner, Kundensuche, Kaufbetrag, Loyalty Preview, Punkte/Stempel bestätigen, Voucher Redemption und Employee Fraud Limits.

### R8 – Customer Portal
Meine Karten, Händlerkarte, QR, Punkte, Stempel, Rewards, Gutscheine, Aktivitäten und Consent.

### R9 – Orders & Refunds
Normalisierte Orders, Order Items, Full/Partial Refund, Reversal Ledger, Debt Balance und Idempotency.

### R10 – Analytics & Operations
Dashboard, KPIs, CSV Import/Export, Monitoring, Backups, Restore Tests, Rate Limiting, Security Hardening und DSGVO Export/Anonymisierung.

### R11 – Wallet & Integrationen
Apple Wallet, Google Wallet, WooCommerce Connector, Shopify, Public API und Webhooks.

### R12 – Growth
Levels, Expiration, Advanced Rule Engine, Segments, Campaigns, Birthday Rewards und Referral.

### R13 – Enterprise
White Label, Custom Domains, SSO/SAML/OIDC, Dedicated Tenant Databases, Advanced Analytics und regionale Deployments.

## MVP-Ziel

Der erste Pilot soll **nicht alle späteren Funktionen enthalten**.

Der erste vollständige Loyalty-Kreislauf lautet:

~~~text
Händler / Test-Tenant
→ Firma + Branding
→ Mitarbeiter
→ Kunde registrieren / anlegen
→ Loyalty-Karte
→ Punkte oder Stempelkarte
→ Mitarbeiter scannt Kunden-QR
→ Punkte/Stempel vergeben
→ Kunde sieht Fortschritt
→ Reward wird erreicht
→ Reward/Gutschein einlösen
→ vollständige Historie und Audit
~~~

Dieser Ablauf muss stabil, sicher und einfach bedienbar sein, bevor größere Integrationen hinzukommen.

## Pilotstrategie

Sobald der Kernflow funktioniert, soll die Plattform früh mit wenigen kontrollierten Pilot-Händlern getestet werden.

Ziele:

- Bedienbarkeit prüfen
- POS-Ablauf unter realen Bedingungen prüfen
- Kundenregistrierung vereinfachen
- Fraud-/Fehlbedienungsrisiken erkennen
- Performance messen
- Händlerfeedback sammeln
- danach Scope gezielt erweitern

## Nicht Teil des ersten Kern-MVP

Bewusst später:

- Apple Wallet
- Google Wallet
- WooCommerce Connector
- Shopify
- vollständige Campaign Engine
- Referral
- komplexe Levels
- Advanced Rule Builder
- Public API
- Public Webhooks
- White Label
- Custom Domains
- SSO
- Dedicated Tenant DB

Die Datenmodelle und Modulgrenzen sollen diese Funktionen bereits berücksichtigen.

## UI/UX-Ziel

Die Händleroberfläche soll nicht wie ein generisches KI-Dashboard wirken.

Designprinzipien:

- klare Hierarchie
- starke Tabellen und Data Grids
- geringe unnötige Dekoration
- konsistentes Design System
- gute mobile Bedienung
- stärkeres Branding bei Loyalty Builder und Customer Card
- Accessibility von Anfang an
- POS besonders schnell und scan-first

## Betriebsmodell

Während Entwicklung:

- ein Development-/Staging-VPS
- separates WordPress-Hosting kann später angebunden werden
- keine echten Kundendaten
- nur Betreiber erhält Infrastrukturzugriff

Vor öffentlichem Go-Live:

- Production von Development/Staging trennen
- eigene Production-Datenbank
- eigene Redis-Instanz
- getrennte Secrets
- Backup plus Restore-Test
- Monitoring und Alerting
- Security Gates
- keine öffentlichen DB-, Redis- oder Worker-Ports

## Verbindliche Change-Safety-Regel

Neue Funktionen dürfen bestehende Funktionen nicht unbeabsichtigt beeinflussen.

Jede relevante Änderung muss prüfen:

- Regression
- Tenant Isolation
- Permissions
- Billing / Entitlements
- API Contracts
- Database Migration
- Ledger-Auswirkungen
- Concurrency
- Idempotency
- UI-Auswirkungen
- Jobs
- Observability
- Rollback

Bevorzugte Patterns sind additive Änderungen, Expand-and-Contract, Feature Flags, Dark Launch, Pilot/Canary, rückwärtskompatible Contracts und automatisierte Regression Tests.

Details: [docs/DEVELOPMENT_RULES.md](docs/DEVELOPMENT_RULES.md)

## Definition of Done

Ein Feature gilt erst als fertig, wenn – soweit relevant – folgende Punkte erfüllt sind:

- fachlich vollständig
- Tenant-Isolation geprüft
- Permission-Verhalten geprüft
- Regression Tests grün
- Idempotency bewertet
- Concurrency bewertet
- Audit/Logging vorhanden
- Feature Flag / Entitlement berücksichtigt
- Responsive UI geprüft
- Error State vorhanden
- Empty State vorhanden
- Migration dokumentiert
- Rollback-/Backout-Weg dokumentiert
- bestehende E2E-Kernflows bleiben funktionsfähig

## Source of Truth

| Bereich | Source of Truth |
| --- | --- |
| Identity / Permissions | SaaS Backend |
| Tenant Status | SaaS Backend |
| Loyalty / Punkte / Stempel | PostgreSQL Ledger |
| Balances | materialisierte Projektion aus Ledger |
| Rewards / Gutscheine | SaaS Backend / PostgreSQL |
| Orders / Refunds | normalisierte SaaS-Projektion |
| Wallet | SaaS Backend; Apple/Google sind Projektionen |
| Billing / Subscription | später externer Provider plus lokale SaaS-Projektion |

## Aktueller Projektstatus

**R0 – Foundation**

Aktuell vorhanden:

- privates GitHub Repository
- initiale Monorepo-Struktur
- Architektur- und Entwicklungsdokumentation
- provider-neutrale Billing-Entscheidung
- geplante Development-/Staging-VPS-Umgebung

Noch nicht produktiv implementiert:

- Framework-Bootstrap
- Docker Compose
- PostgreSQL
- Redis
- Worker
- Authentication
- Tenant-Isolation
- Loyalty-Fachlogik
- POS
- Customer Portal
- Wallet
- WordPress-/Billing-Anbindung

## Nächster technischer Schritt

1. Development-/Staging-VPS bereitstellen.
2. Server absichern.
3. Repository auf dem VPS ausrollen.
4. Docker-/Compose-Grundlage erstellen.
5. Next.js, NestJS, PostgreSQL, Redis und Worker bootstrappen.
6. Healthchecks und Logging einrichten.
7. Danach R1 Identity & Tenancy beginnen.

---

**Status:** Pre-Implementation / R0 Foundation  
**Repository:** IT-Kayali/Loyalty-Platform  
**Architektur:** Modularer Multi-Tenant Monolith  
**Priorität:** sicherer Loyalty-Core vor Wallet-, Shop- und Billing-Integrationen
