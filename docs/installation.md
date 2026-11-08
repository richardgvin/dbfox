# Windows installation

Get the Windows x64 MSI, standalone ZIP or MCP ZIP from
[Releases](https://github.com/richardgvin/dbfox/releases). The first release is
unsigned. Windows may show an unknown-publisher or SmartScreen warning; do
not disable system protections to make an unverified file run.

Download `SHA256SUMS` from the same release and compare the relevant entry:

```powershell
Get-FileHash -Algorithm SHA256 -LiteralPath .\downloaded-file.msi
```

The filename, version and full checksum must match. GitHub's automatic source
ZIP/tar.gz contains this documentation repository, not the application.

## MSI

Run the MSI, select the installation directory and complete the installation.
It installs for all users and requires administrator permission. Launch dbfox
from its shortcut. The Windows WebView2 runtime is required; the installer
includes its bootstrapper, which can require internet access.

The initial supported upgrade baseline is dbfox 0.1.9. A newer MSI preserves
the existing upgrade family and checks the old installation directory.
Always [back up data and its key](https://github.com/richardgvin/dbfox/blob/main/docs/upgrade.md)
before upgrading. Closing or uninstalling the app is not a data backup.

## Standalone ZIP

Extract the entire archive to a writable directory, keeping `web/` next to
`dbfox-server.exe`. In PowerShell, from the extracted directory:

```powershell
.\dbfox-server.exe
```

Open `http://127.0.0.1:7788`. Keep that process running while using the web UI.
The ZIP also includes the `dbfox.exe` CLI. Run `./dbfox.exe --help` for its
commands. This mode does not require installing the desktop application.

Saved connection metadata lives in `%LOCALAPPDATA%\dbfox`, including
`dbfox.db` and `secret.key`. `DBFOX_DATA_DIR` overrides that directory for the
server, desktop and MCP process. Keep database files and the matching key
together; losing the key makes saved credentials unreadable.

For Oracle or Db2, install the vendor's compatible client/ODBC driver
separately. See [driver requirements](https://github.com/richardgvin/dbfox/blob/main/docs/docker.md#external-drivers).

## MCP

MCP is a separate download. Installing the MSI does not configure an AI
client. Follow the [MCP instructions](https://github.com/richardgvin/dbfox/blob/main/docs/mcp.md).
