# Docker & EasyPanel

- Dockerfile: `deploy/Dockerfile.web.subdir` (standalone SSR/Node). Porta 4000.
- Compose base: `deploy/docker-compose.selfhost.root.yml` (web, proxy e sidecars).
- Override na **raiz** `docker-compose.override.yml` com healthwatch/postdeploy.
- Verificação: `docker compose -f deploy/docker-compose.selfhost.root.yml -f docker-compose.override.yml config`.
- No EasyPanel, **não** use `env_file` no web; o painel injeta as envs.
