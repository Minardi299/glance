# Glance dashboard

Personal [Glance](https://github.com/glanceapp/glance) dashboard: YAML config, custom CSS, and Docker Compose to run the app locally or behind a reverse proxy.

## Requirements

- Docker and Docker Compose

## Quick start

1. Copy `.env` from your secrets store (or create one). Glance reads variables like `${MY_SECRET_TOKEN}` from `env_file`; see the [Glance docs](https://github.com/glanceapp/glance) for supported substitutions.
2. Start services:

```bash
docker compose up -d
```

3. Open the dashboard at **http://localhost:8085** (host port `8085` maps to Glance’s `8080` inside the container).

## Layout

| Path | Purpose |
|------|---------|
| `config/glance.yml` | Main config: theme, asset paths, page includes |
| `config/home.yml`, `config/sport.yml` | Page definitions |
| `assets/user.css` | Custom theme (browser may cache; hard refresh after edits) |
| `.env` | Secrets and URLs for widgets (not committed; listed in `.gitignore`) |

## Services

- **glance** — `glanceapp/glance` with `./config` and `./assets` mounted.
- **f1_api** — optional Formula 1 helper API on **localhost:4463** (used if your config points `F1_API_URL` or similar at this service).

The compose file also mounts `/var/run/docker.sock` read-only for the Docker containers widget; remove that volume if you do not need it.
