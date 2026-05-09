# Kodzuverse.Core

Main data services for Kodzuverse.

* **Postgres 18** with **TimescaleDB** (`timescale/timescaledb:latest-pg18`)
* **pgAdmin 4** (`dpage/pgadmin4:9`)

## Quick Start

### 1. Environment variables

Create a `.env` file in the project root:

```env
POSTGRES_USER=myuser
POSTGRES_PASSWORD={YOUR_PASSWORD}
POSTGRES_DB=mydb

PGADMIN_DEFAULT_EMAIL={ANY_EMAIL}        # not validated, just a login id
PGADMIN_DEFAULT_PASSWORD={YOUR_PASSWORD} # min. 6 characters
```

### 2. Create data directories

The bind-mount targets must exist before the first `up` (Some restricted Docker hosts won't auto-create them):

```bash
mkdir -p data/postgres data/pgadmin
sudo chown -R 5050:5050 data/pgadmin   # pgAdmin runs as uid 5050 internally
```

### 3. Start the stack

```bash
docker compose up -d
docker compose logs -f
```

### 4. Enable TimescaleDB in your database

The extension binary is preloaded by the image, but it must be created per database:

```bash
docker compose exec postgres psql -U $POSTGRES_USER -d $POSTGRES_DB \
  -c "CREATE EXTENSION IF NOT EXISTS timescaledb;"
```

Verify:

```bash
docker compose exec postgres psql -U $POSTGRES_USER -d $POSTGRES_DB -c "\dx"
```

## Ports

| Service  | Host port | Container port |
|----------|-----------|----------------|
| Postgres | `5433`    | `5432`         |
| pgAdmin  | `5050`    | `80`           |
