# Supabase — Client/Service Role, Realtime, Storage

- Client (browser): `NEXT_PUBLIC_SUPABASE_URL`, `NEXT_PUBLIC_SUPABASE_ANON_KEY`.
- Server (Service Role): `SUPABASE_SERVICE_ROLE_KEY` (apenas server).
- Realtime em tasks/comentários/presença.
- Buckets: `documents`, `invoices`, `chat-files`, `meeting-recordings` (policies por projeto/room).
- Scripts: `sql_package/v2/setup_all.sql` ou `016..020` em ordem.
