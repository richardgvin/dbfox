# Docker

Download the Compose ZIP from the desired
[release](https://github.com/richardgvin/dbfox/releases). It fixes both images
to the same product version and their SHA-256 digests. Only Linux amd64 is
published initially. The repository's `compose/` directory is the template,
not a ready-to-run version selection.

```sh
cp .env.example .env
docker compose pull
docker compose up -d --wait
docker compose ps
```

The website is `http://127.0.0.1:8080`; the API is on loopback port 7788.
`DBFOX_WEB_PORT` changes the host website port. `DBFOX_SERVER_PORT` changes
the server's internal and loopback host port together. nginx forwards `/api`
to `server` on that port. The template contains only `image:`, never `build:`.

## Storage

Keep project name `dbfox` and volume key `dbfox-data`. Their default Docker
volume name is `dbfox_dbfox-data`, mounted at `/data` in `server`.
The application stores `dbfox.db` and `secret.key` there.

Before migrating a source-built deployment, inspect its actual mount:

```sh
docker inspect "$(docker compose ps -q server)" --format '{{json .Mounts}}'
docker volume inspect dbfox_dbfox-data
```

If the old deployment used a custom project or volume name, keep that name
with `docker compose -p YOUR_EXISTING_PROJECT ...` or an explicit external
volume mapping. Do not create an empty replacement or run `down --volumes`.
See [backup and upgrade](https://github.com/richardgvin/dbfox/blob/main/docs/upgrade.md).

## SQLite and DuckDB files

Host paths are not automatically visible inside containers. Add a bind mount
to the `server` service, such as `/absolute/host/databases:/databases`, and
use `/databases/example.sqlite` or `/databases/example.duckdb` in dbfox.
Set ownership and read/write access for the operation you intend to perform.
Do not place private database files inside an image or the Compose ZIP.

## External drivers

PostgreSQL, MySQL, SQL Server and the other native Rust adapters do not use
the Oracle/Db2 vendor clients. Oracle needs a compatible Oracle Instant
Client; Db2 needs the IBM ODBC/CLI driver and unixODBC configuration. These
vendor drivers are not redistributed with dbfox. Acquire them from their
vendors and check their license, platform, architecture and library paths.
The server image supplies unixODBC and its shared-library prerequisites;
unixODBC alone is not a Db2 driver.

Containers connect to other services by reachable network names, not the
host's `127.0.0.1`. Keep dbfox's published ports local; this deployment does
not add remote-user authentication or authorize internet exposure.
