# ADR-021 – Billing Provider wird nicht zu Projektbeginn angebunden

**Status:** Accepted  
**Datum:** 2026-08-12

## Entscheidung

Die erste Entwicklungsphase erhält keine direkte Stripe-Integration. Billing und Provisioning werden provider-neutral entworfen.

## Begründung

Der Loyalty-Kern soll unabhängig von einem konkreten Payment-/Subscription-Provider entwickelt und getestet werden können. Eine spätere WordPress-/Billing-Anbindung darf keine Umbauten an Tenancy, Loyalty, Permissions oder Entitlements erzwingen.

## Konsequenzen

- Tenant-, Owner-, Plan- und Entitlement-Provisionierung existiert als interne Anwendungsschicht.
- Test-Tenants können zunächst intern erstellt werden.
- Stripe-spezifischer Code darf nicht in Loyalty-, Customer-, IAM- oder Tenancy-Domains gelangen.
- Ein späterer Billing Adapter übersetzt Provider Events in interne Subscription Commands/Events.
- Duplicate Provider Events müssen später idempotent verarbeitet werden.
- Der SaaS-Kern fragt keinen externen Billing Provider bei jedem Request ab.
