# Kodzuverse.Core
Main services for Kodzuverse

* Postgres
* PGAdmin

## Quick Start

Use next environment variables in `.env` file:

* `POSTGRES_PASSWORD={YOUR_PASSWORD}` - password for postgres server
* `PGADMIN_DEFAULT_EMAIL={ANY_EMAIL}` - email for login to PGAdmin (not necessary to be real email)
* `PGADMIN_DEFAULT_PASSWORD={YOUR_PASSWORD}` - password for login to PGAdmin


```
docker-compose up --build -d
```
