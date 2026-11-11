# dbfox

A local workspace for SQL, database exploration and reviewed migrations.

[中文](README.zh-CN.md) · [Website](https://richardgvin.github.io/dbfox-site/en/) · [Downloads](https://github.com/richardgvin/dbfox/releases) · [Installation](docs/installation.md)

![The dbfox SQL workspace](https://richardgvin.github.io/dbfox-site/assets/workspace.jpg)

Explore database objects, run SQL, inspect results and compare migration plans.
The website lists the supported operations for each database: support differs
by engine. Migration execution requires review; MCP tools are read-only or
produce proposals. dbfox runs locally and is not a hosted database service.

## Installation

Download an available version from [Releases](https://github.com/richardgvin/dbfox/releases).
Until a release is published, there are no supported public installers.

- Windows x64: MSI installer or a standalone ZIP with the server, CLI and web UI.
- Docker: Linux amd64 server and web images, with a versioned Compose ZIP.
- MCP: a separate Windows x64 ZIP containing `dbfox-mcp.exe`.
- macOS, Linux desktop and ARM64 packages are not part of the first release.

The first Windows release is **unsigned**. It may show an unknown-publisher or
SmartScreen warning. Verify its SHA-256 against the digest in the release's
Assets list and follow your organization's installation policy. Installing the
MSI does not install or configure the separate MCP package.

For Docker, download and extract the release's Compose ZIP:

```sh
cp .env.example .env
docker compose pull
docker compose up -d --wait
```

Open `http://127.0.0.1:8080`. The template in this repository requires the
version and digests from a release; the downloadable ZIP supplies them.

## User documentation

- [Windows installation and standalone use](docs/installation.md)
- [Docker, storage and external drivers](docs/docker.md)
- [MCP setup and permissions](docs/mcp.md)
- [Backup, upgrade and recovery](docs/upgrade.md)

## Feedback and updates

Use [Issues](https://github.com/richardgvin/dbfox/issues) for installation
questions, bugs and feature requests. Remove connection strings, hostnames,
usernames, passwords and private data before sharing diagnostics.
Report vulnerabilities privately using [SECURITY.md](SECURITY.md).

[Star dbfox on GitHub](https://github.com/richardgvin/dbfox). To receive release
notifications, use **Watch → Custom → Releases** on this repository.
Downloads do not require a Star or a GitHub account.

## License

dbfox binaries are distributed under [MIT](LICENSE). This repository contains
user documentation and deployment configuration, not the product's source
code or build history. [Third-party notices](THIRD_PARTY_NOTICES.md) describe
where to find each release's dependency licenses.
