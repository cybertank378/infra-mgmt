# Infra MGMT

Hyper-V infrastructure inventory and SSL lifecycle platform. Phase 1 targets **one Windows Server Hyper-V host**, **a dedicated Linux management VM**, **manual DNS**, and **end-to-end TLS**. Initial scope: read-only inventory, with future secure certificate orchestration.

## Setup
1. Install Node.js 22+ and PostgreSQL.
2. `npm install`; copy `.env.example` to `.env`, replace all secrets.
3. `npm run db:generate && npm run db:migrate && npm run db:seed`.
4. Register the actual Hyper-V host (its real IP and UUID) in PostgreSQL, and set `HYPERV_HOST_ID`.
5. Run the PowerShell collector on Windows with Hyper-V read permissions and trusted HTTPS to MGMT1.
6. `npm run dev` or `npm run build && npm run start`.

**Security:** browser dashboard is deliberately not enabled until login/session and RBAC exist. The private machine API requires a bearer token. Never deploy unreviewed secrets or disable TLS verification. No production deployment or integration tests have been performed.

See [design.md](design.md), [planning.md](planning.md), [skills.md](skills.md).
