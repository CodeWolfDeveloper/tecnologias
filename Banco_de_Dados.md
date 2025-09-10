# Banco de Dados — Modelagem (Supabase)

Ordem recomendada: `016_complete_database_rebuild.sql` → `017_final_database_fix.sql` → `018_setup_first_admin_with_profile.sql` → `019_kanban_scrum_meetings.sql` → `020_permissions_and_modules.sql`.
Atalho: `sql_package/v2/setup_all.sql`.

## Perfis & Permissões
Tabelas: `user_profiles`, `modules`, `user_modules` (vínculo read/write/admin).

## Projetos & Kanban
Tabelas: `projects`, `project_members`, `boards`, `board_columns`, `tasks`, `task_comments`, `task_tags`/`task_tag_map`, `task_checklists`/`task_checkitems`, `task_watchers`, `task_attachments`.
Função `tasks_reorder(task, column, position)` para drag-and-drop.

## Scrum
Tabelas: `sprints`, `sprint_backlog`, `scrum_events` (planning/daily/review/retro).

## Reuniões
Tabelas: `meeting_rooms`, `meeting_participants`, `meeting_messages`, `meeting_transcripts`, `meeting_minutes`.

## Presença
Tabela: `user_presence` (online/away/busy/offline, last_seen, current_project).

## Notificações
Tabelas: `notification_preferences`, `notification_logs`.

## Primeiro Admin (Token)
Tabelas/Funções: `admin_setup_tokens`, `create_admin_setup_token(master_key)`, `consume_admin_setup_token(token, email, full_name)`.

## Storage
Buckets: `documents`, `invoices`, `chat-files`, `meeting-recordings`. Policies por projeto/room.

## Views
`v_tasks_due_today`, `v_burndown` (exemplos).

> Veja os arquivos `.md` em `docs/` para endpoints e exemplos de uso em cada módulo.
