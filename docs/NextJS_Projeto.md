# Next.js — App Router (SSR/Node)

- Áreas: `/client` e `/internal` com redirecionamento por perfil.
- Variáveis `NEXT_PUBLIC_*` injetadas em runtime via `deploy/entrypoint.sh` → `public/runtime-env.js`.
- Rotas API principais: admin, meet, notifications, kanban/tasks, docs.
- UI com ShadCN, toggle claro/escuro, DnD para Kanban.
