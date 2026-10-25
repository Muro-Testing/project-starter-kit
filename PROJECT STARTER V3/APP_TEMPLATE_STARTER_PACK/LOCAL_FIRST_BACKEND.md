# Local SQL first, Supabase later

Owner-approved framework extension,25 October 2026. Start with a local SQL database, then migrate to Supabase once the app and its workflows are ready. This addition complements the existing app template; it does not change the proprietary licence or replace the original architecture reference.

## Choose the local database deliberately

For an app intended to move to Supabase, prefer local PostgreSQL. Supabase also runs PostgreSQL, so SQL types, relational constraints and much of the policy design transfer directly. SQLite can be useful for a throwaway experiment, but its SQL, concurrency and access-policy differences add conversion work. Do not promise a one-click migration.

Keep the approved prototype as a reference. Build a separate real-app entry point using the same visual components. A service layer should separate rendering from authenticated database operations. For a local browser app, use a loopback API with a least-privileged database login, not database credentials in browser JavaScript.

## Start locally without cloud setup

1. Find the existing database binaries and services before installing or starting anything. Create an isolated cluster or explicitly named development database, with its own port, data directory and credentials. Bind to loopback. Do not alter a client database or repair Docker/WSL as an incidental setup step.
2. Store the data directory, uploads, logs, private configuration and test output outside Git. Source migrations, service code, tests and setup instructions belong in the app repository. Record the database version and data location. Never reset an existing nonempty data directory to make a script pass.
3. Write numbered SQL migrations. Keep business records and identity mapping in the business schema. Keep local password hashes and sessions in a separate local-auth schema. Do not use a PIN, developer-email detection or a browser role switch as the security boundary.
4. Implement one persistent journey: sign in, create a project, reload, sign out and in, and see the same record. Then verify a second identity can access only its own assigned records. Test actual direct API/database access, not only hidden buttons.
5. Add private files through an authorised backend flow. Validate size/signature/type, use opaque object IDs, preserve the display name separately and recheck membership for downloads. An object must belong to the same project/version as its database record. Preserve old versions and approvals when creating a revision.
6. Make a database-and-files backup, restore into a different isolated database, and compare relationships and object bytes. A SQL dump alone does not contain local object files.

For the Forme course implementation, local PostgreSQL17 and Node22 run this route. Its SQL/API/browser acceptance tests and backup restore cover fictional admin, two clients and an unassigned identity. This is a tested course implementation, not certification of every module in the original template or a production hosting claim.

## Keep migration boundaries explicit

| Component | Local development | Later Supabase step |
| --- | --- | --- |
| Records | PostgreSQL business schema and constraints | Apply reviewed migrations and import business rows, preserving IDs and checking counts/relationships |
| Identity | Local password/session adapter | Provision Supabase Auth identities and map each `auth.users.id` to the existing profile; require a fresh sign-in or password setup |
| Authorisation | Server sets authenticated actor inside a transaction; non-owner runtime role enforces RLS | Replace actor adapter with verified `auth.uid()` mapping; grant only intended roles and rerun cross-client tests through actual JWTs |
| Files | Private disk objects keyed by immutable IDs | Upload objects to a private bucket; verify hashes and metadata, replace storage adapter and test private downloads |
| Secrets | Private server configuration outside Git | Store appropriate server secrets in the target runtime; no service-role/secret key in the browser |
| Sessions | Local hashed session tokens | Expire local sessions; do not copy them to Supabase Auth |
| AI/Gmail | Disconnected until their own integration step | Replace service adapters deliberately; OAuth tokens remain server-side and sends require exact-payload review |

Do not import local credentials/session tables into exposed Supabase schemas. Do not expose local SECURITY DEFINER upload functions as a public Storage API without adapting their validation and object-registration contract. Client-editable metadata must never assign admin permissions. Database owner/service-role bypasses must never be used as the normal client account in isolation tests.

## Cut over only after a rehearsal

Make a verified recovery backup. Stop writes for the final copy, transfer business rows and files, map identities and validate two clients plus an unassigned account. Confirm login, persistence, new revisions, approval history, private downloads and failure recovery. Only then change the application's provider configuration. Keep the original local data and migration manifest until the owner accepts the migrated result. Never silently destroy originals, rotate credentials, send invitations or publish a deployment during migration.

## Course sequence

Prototype approval → local PostgreSQL and data model → real login/roles → persistent project → private files/reviews → API integration → Supabase migration rehearsal → hosting and final independent exercise.

Teach each step with an explicit prompt button, the correct Codex/Claude project chat, paste/send/wait/check, and return-to-workbook instruction. Learners should see the concrete record or file that proves completion before proceeding. Keep cloud accounts and any spending decisions out of the initial local database lesson.

## Completion checks

- [ ] Database data and private runtime are outside Git; only known safe source is committed.
- [ ] Unassigned and cross-client requests fail at the database/API boundary.
- [ ] Records and private objects survive restart; version-specific reviews cannot approve a later revision.
- [ ] Backup plus object files restore into a separate database with matching relationships and bytes.
- [ ] Supabase identity/storage/policy adapters are mapped and tested before a cloud cutover.
- [ ] Real invitations, email sends and public hosting retain their own explicit authorisation.
