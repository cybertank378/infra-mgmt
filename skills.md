# SKILLS — Project Implementation Rules

1. **Inspect first:** read design.md, planning.md and neighboring modules. Keep file structure consistent; never replace existing behavior without impact assessment.
2. **Hexagonal backend:** domain types and Zod → repository contracts → use cases → Prisma/infra adapters → HTTP presentation. Business logic cannot depend on React. Stable Hyper-V GUIDs, transactional upsert and explicit error types.
3. **Atomic UI:** organisms compose molecules, molecules compose atoms. Reuse shared UI components and API hooks; avoid raw dummy lists, unstable React keys, alert(), and routing into missing pages. Responsive compact layout, accessible feedback, placeholders for empty state.
4. **Data freshness:** user- and infrastructure-sensitive data use no-store and safe refresh. Mutations trigger revalidation, server-side guards and audit logs.
5. **Security:** default-deny, enforce trusted HTTPS and HMAC with time bounds, replay IDs and secret rotation. Secrets never enter logs, repository, UI or error responses. Per-target minimum permissions and TLS verification.
6. **Operations:** staging and validation before certificate activation; one HAProxy node at a time; verify health then continue; rollback on failure. Never use NFS as a broadly readable private-key share.
7. **Tests:** Prisma validate, TypeScript, lint, build and unit/integration tests (auth denial, replay, stale snapshot, no false status). Do not claim tests passed unless executed. Do not commit without user instruction.
