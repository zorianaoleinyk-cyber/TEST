# Odoo 19 Community test environment

A local Odoo 19 Community and PostgreSQL setup managed with Docker Compose. The Compose file initializes the Odoo database `odoo` with Inventory, Sales, Purchase, and Manufacturing modules and exposes the web interface on port 8069.

## Requirements

- Windows with Docker Desktop configured to use WSL 2
- Git (for repository work)

## Start locally

From this directory, run:

```powershell
docker compose up -d
```

Then open <http://localhost:8069> in a browser. On first start, the one-shot `odoo-init` service initializes the database before the web service starts. Initialization may take several minutes. Check progress with `docker compose ps` and `docker compose logs -f odoo-init`.

The Compose setup uses named Docker volumes for PostgreSQL and Odoo data. These volumes persist independently from the containers. `docker compose down` stops and removes containers while keeping volumes. **Do not run `docker compose down -v` unless you intend to permanently remove the stored database and Odoo files.**

## Before publishing or sharing

Credentials are read from the local `.env` file, which is excluded from Git. Copy `.env.example` to `.env` and set the same strong password for `POSTGRES_PASSWORD` and `ODOO_DB_PASSWORD`. Commit only `.env.example`, never `.env`. If a credential was published previously, rotate it before sharing the repository.

`JOURNAL.md` is intentionally included in the repository at the user's request. Review its contents before public release. Do not add database dumps, Docker volume contents, `.env`, credentials, or other private local data to the repository.

## Included Codex skill

The reusable `daily-work-report` skill is stored under `skills/daily-work-report/`. To install it for a Codex user account, copy that folder into `~/.codex/skills/` (on this Windows setup: `%USERPROFILE%\.codex\skills\`).

