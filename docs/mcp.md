# MCP setup

Download the Windows x64 MCP ZIP from the same
[release](https://github.com/richardgvin/dbfox/releases) as your application.
Verify `SHA256SUMS`, extract it, and locate `dbfox-mcp.exe`. You do not need
Rust or `cargo build`. The MSI and standalone web server do not configure an
AI client's MCP connection automatically.

Configure a client that supports stdio MCP servers. Replace the paths below
with absolute paths on your computer:

```json
{
  "mcpServers": {
    "dbfox": {
      "command": "C:\\Tools\\dbfox-mcp\\dbfox-mcp.exe",
      "args": [],
      "env": {
        "DBFOX_DATA_DIR": "C:\\Users\\YOUR_USER\\AppData\\Local\\dbfox"
      }
    }
  }
}
```

If the desktop app uses the default data directory under the same Windows
account, `env` can be omitted. If it uses `DBFOX_DATA_DIR`, the MCP process
must use that same directory. Do not copy `secret.key` into the AI client's
configuration or put credentials in command-line arguments.

Save a database connection in dbfox and review its agent-access setting.
Connections hidden from agents are not listed. Read-only connections expose
metadata and permitted read queries; tools can generate SQL or migration
proposals but do not execute writes. Database grants remain an independent
boundary: use a least-privilege database account.

Restart or reconnect the client's MCP server, confirm that `list_connections`
shows the expected connection, and run a harmless metadata/read operation
against a synthetic or otherwise appropriate database. An empty connection
list can mean a different data directory or disabled agent access.

The process uses standard input/output for the protocol and standard error
for diagnostics. Do not wrap it in a script that prints banners to stdout.
Do not publish data-directory contents or unredacted query results when
reporting problems.
