# Verbindliche Entwicklungsregeln

Diese Regeln gelten für jede neue Funktion und jeden Merge.

## 1. Keine unbeabsichtigten Nebenwirkungen

Neue Funktionen dürfen bestehende Funktionen, Datenmodelle, APIs, Rollen, Abonnements, Ledger oder Workflows nicht stillschweigend verändern.

## 2. Modularität

- Features werden in klar abgegrenzten Fachmodulen umgesetzt.
- Kommunikation erfolgt über definierte Interfaces/Contracts.
- Keine versteckten Querabhängigkeiten zwischen Domains.

## 3. Rückwärtskompatibilität

- Bestehende API-Contracts bleiben kompatibel.
- Breaking Changes benötigen Versionierung und einen expliziten Migrationspfad.
- Additive Änderungen werden bevorzugt.
- Größere DB-Änderungen verwenden Expand-and-Contract.

## 4. Tenant Isolation

Jedes tenant-gebundene Feature muss prüfen:

- API Scope
- DB/RLS Scope
- Cache Keys
- Queue/Job Payloads
- Files/Storage Keys
- Imports/Exports
- Analytics
- Integrationen/Webhooks

Cross-Tenant-Tests sind Pflicht.

## 5. Permissions

Neue Aktionen erhalten explizite Permissions. Eine neue UI-Funktion erweitert Rollen oder Navigation niemals automatisch.

## 6. Feature Flags & Entitlements

Neue Funktionen müssen kontrolliert aktivierbar sein. Planabhängige Features und Limits werden serverseitig geprüft.

## 7. Idempotency & Concurrency

Bei relevanten Funktionen muss definiert und getestet sein:

- Retry
- Doppelclick
- Duplicate Webhook/Event
- parallele Requests
- Locking/atomare Updates

## 8. Ledger-Regel

Punkte-, Stempel-, Reward- und Voucher-Auswirkungen dürfen nicht durch direkte Saldenmanipulation umgesetzt werden. Die jeweilige Domain- und Ledger-Logik ist zu verwenden.

## 9. Migrationen

- Migrationen müssen kontrolliert und nachvollziehbar sein.
- Rollback/Recovery muss vor Deployment bewertet werden.
- Keine destruktive Schemaänderung ohne Migrationspfad.

## 10. Observability

Kritische Aktionen erhalten strukturierte Logs und – wo erforderlich – Audit-Einträge, Metriken und Alerts.

## Pflichtprüfung vor Merge

- [ ] Regression bewertet und Tests vorhanden
- [ ] Tenant Isolation geprüft
- [ ] Permissions geprüft
- [ ] Billing/Plan/Entitlement geprüft
- [ ] API Contract geprüft
- [ ] Datenbank/Migration/Index/Constraint geprüft
- [ ] Ledger-Auswirkungen geprüft
- [ ] Concurrency geprüft
- [ ] Idempotency geprüft
- [ ] UI-Ausblendung/Feature Flag geprüft
- [ ] Jobs/Retry/Backoff geprüft
- [ ] Logging/Audit/Observability geprüft
- [ ] Mobile/Responsive geprüft, falls UI
- [ ] Error/Empty States definiert
- [ ] bestehende E2E-Kernflows bleiben grün
