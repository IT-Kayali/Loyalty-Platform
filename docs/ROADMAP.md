# Entwicklungsroadmap

## R0 – Foundation

Repository, Branch-/Release-Strategie, Umgebungen, Docker, Config/Secrets, PostgreSQL, Redis, BullMQ Worker, Reverse Proxy, Logging, Healthchecks und CI/CD.

**Abnahme:** reproduzierbare Entwicklungsumgebung ohne echte Kundendaten.

## R1 – Identity & Tenancy

Login, Sessions, Tenant Context, Tenant Isolation/RLS, RBAC, Permissions, Filial-Scope und Audit.

**Abnahme:** Test-Tenants können ausschließlich eigene Daten sehen und verändern.

## R2 – Provider-neutrale Provisioning Foundation

Tenant/Owner/Plan/Entitlement-Lifecycle wird intern implementiert, ohne direkte Stripe-Abhängigkeit. Test-Tenants können über Super Admin oder Seed/Test-Mechanismus provisioniert werden. WordPress/Billing-Adapter folgt später.

## R3 – Merchant Core

Unternehmen, Branding, Filialen, Mitarbeiter, Rollen und Kundenverwaltung.

## R4 – Loyalty Core

Händler-Loyalty-Karte, Punkteprogramme, immutable Points Ledger, materialisierte Balances und QR-Identifier.

## R5 – Stamp Cards

Templates, Gallery, Builder, Live Preview, Regeln, Limits, Zyklen und immutable Stamp Ledger.

## R6 – Rewards & Vouchers

Reward Definition, Customer Reward Snapshot, Voucher Issue/Redeem/Expire und Double-Spend-Schutz.

## R7 – POS

Scan-first POS, Kundensuche, Kaufvorschau, Punkte/Stempel und Voucher Redemption.

## R8 – Customer Portal

Meine Karten, QR, Punkte, Stempel, Rewards, Vouchers, Activity und Consent.

## R9 – Orders & Refunds

Orders, Items, Full/Partial Refunds, Reversals, Debt Balance und Idempotency.

## R10 – Analytics & Operations

Dashboard, Aggregates, Import/Export, Monitoring, Backups, Restore Tests, Rate Limits und DSGVO-Werkzeuge.

## Später

Wallet, WooCommerce, Shopify, Public API/Webhooks, Levels, Expiration, Campaigns, Segments, White Label, SSO und Dedicated Databases.
