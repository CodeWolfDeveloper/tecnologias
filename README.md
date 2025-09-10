# CodeWolf — Plataforma de Desenvolvimento (Self‑Host)

Este repositório consolida **tudo** para rodar a plataforma de desenvolvimento da CodeWolf em ambiente **100% self‑host** (Next.js SSR/Node, Supabase, LiveKit, EvolutionAPI/WhatsApp, GitHub, IDE web com code‑server, Swagger, Sentry opcional, Workers BullMQ opcionais).

## Visão Geral
- Áreas separadas: **Cliente** (`/client`) e **Interna** (`/internal`) com redirecionamento por perfil.
- Menu dinâmico por permissões (catálogo `modules` + `user_modules`).
- Projetos com **Kanban** e **Scrum**, Realtime e RLS.
- Reuniões via LiveKit (`/meet?room=...&name=...`) com token (`/api/meet/token`); pipeline de **transcrição/ATA** com Groq.
- Notificações (e‑mail/WhatsApp via EvolutionAPI) com dispatcher unificado.
- Anexos no Supabase Storage (buckets: `documents`, `invoices`, `chat-files`, `meeting-recordings`).
- IDE Web (code‑server) e integração GitHub (OAuth/App + webhook).
- Swagger/OpenAPI em `/api/docs`. Sentry & Workers BullMQ opcionais.

## Pré‑requisitos
- Node.js 18+, Docker + Compose 2.20+, conta Supabase. (Opcional) LiveKit, EvolutionAPI, Sentry, Redis, code‑server.

## Variáveis de Ambiente (exemplo)
```
NODE_ENV=production
PORT=4000
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=
NEXT_PUBLIC_APP_URL=
NEXT_PUBLIC_SITE_URL=
APP_DOMAIN=
APP_WWW_DOMAIN=
GROQ_API_KEY=
GROQ_TEXT_MODEL=llama-3.1-70b-versatile
GROQ_STT_MODEL=whisper-large-v3
EVOLUTIONAPI_BASE_URL=
EVOLUTIONAPI_TOKEN=
EVOLUTIONAPI_INSTANCE_ID=
EVOLUTIONAPI_VARIANT=sendText
EVOLUTIONAPI_AUTH_HEADER=apikey
NEXT_PUBLIC_LIVEKIT_URL=
LIVEKIT_API_KEY=
LIVEKIT_API_SECRET=
GITHUB_CLIENT_ID=
GITHUB_CLIENT_SECRET=
GITHUB_WEBHOOK_SECRET=
GITHUB_APP_ID=
GITHUB_APP_PRIVATE_KEY_BASE64=
NEXT_PUBLIC_CODE_SERVER_URL=
WORKSPACE_BASE=/home/coder/workspaces
CODE_SERVER_PASSWORD=
SMTP_HOST=
SMTP_PORT=465
SMTP_USER=
SMTP_PASS=
SMTP_FROM=
SMTP_SECURE=true
SENTRY_DSN=
SENTRY_ENVIRONMENT=production
SENTRY_TRACES_SAMPLE_RATE=0.1
SENTRY_PROFILES_SAMPLE_RATE=0.1
```
> Em produção, o EasyPanel injeta as envs; `deploy/entrypoint.sh` gera `public/runtime-env.js` para o **front** ler `NEXT_PUBLIC_*` em **runtime**.

## Banco de Dados (Supabase)
1. Execute `sql_package/v2/setup_all.sql` (ou `016..020` em ordem) no SQL Editor.
2. Crie buckets `documents`, `invoices`, `chat-files`, `meeting-recordings` e aplique policies.
3. Configure RLS conforme `docs/Supabase.md` e `docs/Storage_Buckets.md`.
4. Gere o primeiro admin com token (ver `docs/Banco_de_Dados.md`).

## Build & Run
**Local**
```
npm ci
npm run dev
# build SSR/Node
npm run build && npm start
```
**Docker**
```
docker compose -f deploy/docker-compose.selfhost.root.yml up -d --build
```
**EasyPanel**
- Dockerfile: `deploy/Dockerfile.web.subdir` (porta 4000).
- Variáveis no painel. (Opcional) `docker-compose.override.yml` na **raiz** com healthwatch/postdeploy.

## Rotas/Endpoints principais
- `/api/admin/users/create`, `/api/admin/access/upsert`, `/api/me/modules`
- `/api/meet/token`, `/api/meet/transcribe`, `/api/meet/ingest`
- `/api/notifications/dispatch`
- `/api/kanban/board`, `/api/tasks/reorder`, `/api/tasks/bulk-create`
- `/api/docs`, `/healthz`

## Documentação por Ferramenta
Veja a pasta `docs/`:
- IA_Groq.md, NextJS_Projeto.md, Supabase.md, EvolutionAPI.md, LiveKit.md,
- GitHub_Integracao.md, CodeServer_IDE.md, Docker_EasyPanel_Deploy.md,
- Workers_BullMQ.md, Sentry.md, Storage_Buckets.md, Swagger_OpenAPI.md
