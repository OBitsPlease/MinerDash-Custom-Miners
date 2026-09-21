# Miner Dash Custom Miners

This repository is the approved community registry for Miner Dash custom miner
integrations. Every Miner Dash controller periodically reads `catalog.json`.
Approved entries automatically appear under **Miner Dash community miners** in
the Custom Miner Lab and Flight Sheet miner lists.

The main Miner Dash application will be published at
[OBitsPlease/Miner-Dash](https://github.com/OBitsPlease/Miner-Dash) when version
1.0 is ready.

## Submission requirements

1. Host the original Linux executable or `.tar.gz` package at a stable public
   HTTPS URL, preferably an official GitHub release.
2. Do not include wallets, credentials, worker names, private endpoints, or
   tracking identifiers.
3. Choose `package_format: "binary"` for a self-contained executable, or
   `package_format: "tar.gz"` for a complete directory bundle.
4. Set `executable_name` to the entry-point basename. For bundle packages, set
   `entry_point` to its safe relative archive path and `package_sha256` to the
   SHA-256 of the complete compressed archive.
5. Calculate SHA-256 for the executable selected by `entry_point` and place it
   in `executable_sha256`.
6. Use one argument per `default_arguments` array item.
7. Document the upstream source, license, developer fee, supported hardware,
   and algorithm.
8. Submit the new entry for review. Do not edit or replace another developer's
   package.

## Supported placeholders

- `{POOL}` - complete pool URL
- `{POOL_ENDPOINT}` - pool host and port
- `{WALLET}` - wallet address or resolved wallet template
- `{WORKER}` - rig name
- `{PASSWORD}` - pool password
- `{COIN}` - coin ticker
- `{ALGORITHM}` - flight-sheet algorithm

## Security and review

Miner Dash downloads packages without running installer scripts. Binary mode
extracts only `executable_name`. Bundle mode preserves regular files and
directories, rejects absolute paths, traversal, links, devices, and oversized
content, then launches only `entry_point`. It verifies both `package_sha256` and
`executable_sha256` and rolls back the complete installed directory when a new
version fails to start.

Reviewers must verify package provenance, licensing, executable behavior,
network destinations, developer fees, and the submitted hash before merging an
entry into `catalog.json`.

Bundle entries may define environment variables and one supported local
statistics endpoint with `environment`, `stats_type`, and `stats_url`.
Hive-specific configuration, run, statistics, and supervisor callbacks are
never executed. A reviewer must translate those behaviors into native Miner
Dash arguments, environment settings, and statistics configuration.
