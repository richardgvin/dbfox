# Security reporting

Do not put vulnerabilities, credentials or private database data in public
Issues. Use [GitHub private vulnerability reporting](https://github.com/richardgvin/dbfox/security/advisories/new).
If GitHub does not offer the reporting form, private reporting has not yet
been enabled; do not substitute a public report containing sensitive details.

Include the dbfox version, operating system, affected deployment mode and a
minimal reproduction using synthetic data. Remove connection strings,
hostnames, usernames, passwords, tokens and business data. Never attach
`secret.key`, a live `dbfox.db`, or an entire data directory.

dbfox is intended for local use. Keep the default loopback bindings. Opening
its API or web port to untrusted networks is not a supported deployment.
