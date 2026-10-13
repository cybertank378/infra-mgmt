# PLANNING

## Phase 1 — Hyper-V inventory (this branch)
- [x] Repository scaffold, Prisma domain models, 15 VM seed, private overview API.
- [x] PowerShell read-only collector; HMAC authenticated ingestion; snapshot deduplication.
- [ ] Login/session, RBAC, UI data hooks and enable secured responsive dashboard.
- [ ] Register real Hyper-V IP/ID; correlate discovered GUIDs to inventory with approval.
- [ ] Health probes, stale/offline evaluator and paginated server APIs.
- [ ] Prisma migrations, integration tests, real Windows/Linux end-to-end verification and deployment hardening.

**Done when:** all 15 VM identities are verified, no hardcoded health values, unauthorized requests rejected, observed VM states are real, tests green.

## Phase 2 — SSL management
- [ ] Manual DNS-01 flow; expiration monitoring; ACME certificate lifecycle.
- [ ] Internal CA with unique key per backend; vault storage.
- [ ] Versioned cert artifacts, renewal and revocation.

## Phase 3 — Deploy SSL to LB and backend
- [ ] Restricted SSH orchestration + idempotent worker.
- [ ] Nginx config checks and internal CA trust.
- [ ] HAProxy deployment LB standby-first with health validation, secure rollback and audit.
- [ ] Verify served fingerprint/SNI and end-to-end certificate chain.

## Phase 4 — Ops and remote control
- [ ] JEA-constrained Hyper-V operations, approvals, alerting and DR.
- [ ] Monitoring reports, high-availability risk review and backups.

No production readiness claim until actual tests. A single physical Hyper-V host remains a single point of failure.
