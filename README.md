# Miner Dash Custom Miners

This repository is the approved community registry for Miner Dash custom miner
integrations. Every Miner Dash controller periodically reads `catalog.json`.
Approved entries automatically appear under **Miner Dash community miners** in
the Custom Miner Lab and Flight Sheet miner lists.

## Submission requirements

1. Host the original Linux executable or `.tar.gz` package at a stable public
   HTTPS URL, preferably an official GitHub release.
2. Do not include wallets, credentials, worker names, private endpoints, or
   tracking identifiers.
3. The archive must contain a self-contained executable whose basename exactly
   matches `executable_name`.
4. Calculate SHA-256 for the extracted executable, not the compressed archive,
   and place it in `executable_sha256`.
5. Use one argument per `default_arguments` array item.
6. Document the upstream source, license, developer fee, supported hardware,
   and algorithm.
7. Submit the new entry for review. Do not edit or replace another developer's
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

Miner Dash downloads the package without running installer scripts, extracts
only `executable_name`, calculates its SHA-256, and rejects the installation if
it differs from `executable_sha256`.

Reviewers must verify package provenance, licensing, executable behavior,
network destinations, developer fees, and the submitted hash before merging an
entry into `catalog.json`.

Multi-file packages that require bundled libraries, helper programs, or shell
callbacks are not accepted by schema version 1. They require a reviewed native
Miner Dash adapter.
