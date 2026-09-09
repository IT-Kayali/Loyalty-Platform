# Loyalty Platform

Multi-Tenant Loyalty & Rewards SaaS.

Dieses Repository enthält die technische Umsetzung der Loyalty-SaaS-Plattform. Die Architektur folgt einem modularen Monolithen mit klar getrennten Fachdomänen und einer strikten Multi-Tenant-Isolation.

## Zielarchitektur

- **Frontend:** Next.js / React / TypeScript
- **Backend/API:** NestJS / TypeScript
- **Datenbank:** PostgreSQL
- **Cache & Jobs:** Redis + BullMQ
- **Deployment:** Docker / Docker Compose
- **Source Control / CI:** GitHub / GitHub Actions
- **Öffentliche Verkaufs- und Account-Schicht:** WordPress (spätere Anbindung)
- **Billing Provider:** bewusst noch nicht fest verdrahtet; Integration erfolgt später über einen Adapter

## Repository-Struktur

```text
loyalty-platform/
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
├─ infrastructure/
├─ docs/
└─ tooling/
```

## Entwicklungsreihenfolge

1. **R0 – Foundation**: Repository, Umgebungen, Config, Docker, DB, Redis, Worker, Logging, CI/CD.
2. **R1 – Identity & Tenancy**: Auth, Sessions, Tenant Context, RLS, RBAC, Location Scope, Audit.
3. **R2 – Provisioning Foundation**: Provider-neutrale Tenant-/Owner-/Plan-Provisionierung; WordPress/Billing-Anbindung später.
4. **R3 – Merchant Core**: Firma, Branding, Filialen, Team, Kunden.
5. **R4 – Loyalty Core**: Händlerkarte, Punkte, Ledger, Balances, QR.
6. **R5 – Stamp Cards**: Templates, Gallery, Builder, Preview, Rules, Cycles.
7. **R6 – Rewards/Vouchers**.
8. **R7 – POS**.
9. **R8 – Customer Portal**.
10. **R9 – Orders/Refunds**.
11. **R10 – Analytics/Ops**.

## Verbindliche Entwicklungsregel

Neue Funktionen müssen modular, tenant-sicher, rückwärtskompatibel und ohne unbeabsichtigte Nebenwirkungen eingeführt werden. Details stehen in [`docs/DEVELOPMENT_RULES.md`](docs/DEVELOPMENT_RULES.md).

## Aktueller Status

**R0 – Foundation wird vorbereitet.** Noch keine produktive Implementierung und keine echten Kundendaten.
