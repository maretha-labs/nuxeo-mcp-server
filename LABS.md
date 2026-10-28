# Maretha Labs / Hyland collaboration

Maretha partnered with Hyland on Nuxeo MCP. Hyland maintains the canonical repository:
https://github.com/nuxeo/nuxeo-mcp-server. This repository is a GitHub fork of it.

The `labs` default branch is upstream commit `3c06691fe1ab99160bb10be83d2f49205ba5c819`
plus one Labs commit: this documentation, a LICENSE file, SECURITY.md and fork-safe workflow
triggers. `main` mirrors upstream; pull requests to Hyland start from topic branches of it.

Use Hyland upstream for canonical development and current release information. This fork
is for Maretha examples and collaboration; it is not a competing supported distribution.
Original author history and attribution are preserved. No runtime code changes were made
for the Labs release.

## Maretha contributions upstream

Maretha contributed natural-language search that compiles to NXQL, OAuth2 sign-in with
token storage, and the search-engine passthrough to the canonical project. See
[the commits](https://github.com/nuxeo/nuxeo-mcp-server/commits?author=espa77).

## Get started

```bash
git clone --branch labs https://github.com/maretha-labs/nuxeo-mcp-server.git
cd nuxeo-mcp-server
uv sync --frozen --extra dev
uv run nuxeo-mcp --help
```

If `nuxeo-mcp` fails with `cannot import name 'JWT' from 'jwt'`, the `jwt` and `pyjwt`
dependencies both install into `jwt/` and the wrong one was written last. Restore it with
`uv pip install --reinstall jwt==1.4.0`.

Configure a least-privilege Nuxeo account and the required transport/authentication before
connecting a client. The upstream README explains the account and tool permissions. Do not
use local-development defaults against production. An exposed HTTP server needs an appropriate
network and client-authentication boundary; a tool being available does not authorize every
user to execute it. No credentials or production data are included in this Labs preparation.

## Validation and maintenance

Validated 2026-10-28. Hyland's CI checks passed on the upstream reference commit. Locally
(macOS arm64, Python 3.13, clean `uv sync --frozen --extra dev` plus the `jwt` reinstall
above), 112 unit tests passed and 19 integration tests were skipped; the source distribution
and wheel built successfully. Upstream static checks remain failing: mypy reports 136 errors
in 13 source files, Black would reformat 48 files, and isort reports import-order differences
in 46. These baseline findings were not changed for Labs. No live Nuxeo or hosted-model
integration was certified. GitHub Actions is disabled for this fork; on `labs`, workflow
triggers are also manual only and the image-publishing job is disabled, so nothing here can
publish to Hyland infrastructure. Upstream setup
instructions and scripts remain reference material, not an instruction to deploy to its accounts.

Future upstream changes should be reviewed before integration. See SECURITY.md for reporting.
