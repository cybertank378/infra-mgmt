# DESIGN — Infra MGMT

## Deployment
- Hypervisor: single physical Windows Server Hyper-V (single failure domain).
- Dedicated MGMT1 Linux VM: Next.js API/UI + PostgreSQL; management IP assigned only after address conflict check.
- Inventory groups: LB1 .21, LB2 .22; LMS1–3 .11–13; UJIAN1–3 .30–32; ERP1–3 .2–4; LOMBA1–3 .246–248; SHARE1 .60; all 192.168.100.0/24.
- Manual DNS means public ACME DNS-01 may require manual TXT challenge on each issuance/renewal.
- End-to-end TLS: public trusted TLS at HAProxy; separately issued internal-CA identities at Nginx backends. HAProxy verifies each backend's certificate, SAN, hostname and chain; never `verify none`.

## Component boundaries
- React UI → authenticated Next.js routes → application use cases → Prisma repository.
- Windows Task Scheduler → PowerShell read-only Get-VM → trusted HTTPS HMAC snapshot ingestion → transactional VM upsert.
- Future ACME/PKI and SSH deploy worker operate asynchronously, never from React.

## Security and recovery
Authentication before exposing infrastructure views. Collector requires exact UTF-8 HMAC + timestamp and snapshot id for replay protection. Credential and private-key material must be encrypted in a secret store; do not store secrets in git/audit logs. Limit firewall paths; least-privileged collector and deployer. No bulk reloading both HAProxy nodes. Deployment stages → validates → checks standby → switches one LB → verifies health → rolls to peer; rollback restores last valid bundle. NFS must not expose readable private keys.

## Data model
Hypervisor has VirtualMachine (unique Hyper-V GUID). Server is distinct and is linked after explicit reconciliation; do not infer identity from IP. Service health remains UNKNOWN until actually tested. Certificate and deployment tables reserve future work; certificate version history follows in Phase 2.

## UI system
Responsive max-width 1600px; dashboard extends usable viewport instead of narrow centered layout. Components: atoms/molecules/organisms, shared controls, hook/API-sourced state, no dummy health or fake key, accessible loading/error/empty states. Preserve meaningful empty-state illustrations.

## Gates
Run prisma validate/generate, TypeScript, build, lint, auth-negative integration tests, collector replay tests and production rollback drills before release.
