# Backup, upgrade and recovery

Back up the entire data directory, including `dbfox.db`, its SQLite sidecar
files if present, and the matching `secret.key`. Saved credentials cannot be
recovered from the database alone. Back up external SQLite/DuckDB files
separately. Store backups outside the directory or volume being upgraded.

## Windows

Close dbfox and stop standalone/MCP processes using the same directory.
Copy `%LOCALAPPDATA%\dbfox` (or the directory set by `DBFOX_DATA_DIR`) to a
dated backup location. Then run the new MSI or extract a new standalone/MCP
ZIP in a separate program directory. Start the new version and check saved
connections. The installation directory is not the data directory.

## Docker

First record the existing project and volume names, image digests and
configuration. In its Compose directory, stop the server and web services
before copying the application data:

```sh
docker compose stop web server
backup_dir="$PWD/dbfox-backup-$(date +%Y%m%d-%H%M%S)"
mkdir "$backup_dir"
docker compose cp server:/data/. "$backup_dir/"
test -s "$backup_dir/dbfox.db"
test -s "$backup_dir/secret.key"
```

Keep this backup and the old Compose files together. Secure them as database
credentials. Download the new release's Compose ZIP, preserve the original
project/volume and port settings, then run:

```sh
docker compose pull
docker compose up -d --wait
docker compose ps
```

Confirm the existing connection list and one permitted database operation.
Recreating containers must keep the same volume and key. Do not use
`docker compose down --volumes` as part of upgrading.

## Recovery

If startup or data compatibility fails, stop the new server and preserve its
data for diagnosis. Restore a *copy* of the pre-upgrade data and matching key
to a dedicated recovery directory or volume, then run the old pinned images
against that copy. Verify the connection list and credential decryption
before redirecting the original deployment. Do not overwrite the only copy
of either the backup or the upgraded data.

Changing an image tag back does not undo database migrations. Image rollback
and data recovery are separate operations. If the website's recommendation
is withdrawn, choose the documented replacement release; never replace
files inside an immutable published release.
