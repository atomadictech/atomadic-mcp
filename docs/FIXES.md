# What was broken, and what we changed

A record of real faults found by actually using this thing from the outside, with the evidence. Written so the next person does not rediscover them.

## 2026-10-26

### 1. `atomadic.tech/docs/mcp` returned 404, and `llms.txt` sent people there

**Symptom.** `https://atomadic.tech/llms.txt` links the MCP plugin install guide at `https://atomadic.tech/docs/mcp`. That path returned `404` with a 9-byte body. `docs.html` (the real docs shell, 17,907 bytes) contains the string `mcp` zero times. The page was never written, not merely mislinked.

**Also broken.** The PyPI long description for `aaaa-nexus-mcp` 0.1.1 links its `Documentation` field to the same dead path, and its `Repository` field points at `github.com/AAAA-Nexus/aaaa-nexus-mcp`, which returns 404 for anyone without access. So a stranger following the package page hits two dead ends in a row.

**Root cause.** Docs were authored as prose inside the package description and never published as site pages. No route exists inside the site program for `/docs/mcp`, so no amount of retrying the URL would fix it.

**What we did.** Wrote the missing page from the package's actual code, not from marketing copy: entry point is `python -m aaaa_nexus_mcp` (stdio), it requires Python 3.12+ and pulls in `mcp[cli]` and `httpx`, and the env vars come from `aaaa_nexus_mcp/config.py`. Published at `docs/mcp.html` in this repo.

**Still open.** `atomadic.tech/docs/mcp` needs a redirect rule to that page. Until then the link in `llms.txt` and on PyPI stays dead. The `llms.txt` text itself lives inside the deployed site program and needs a separate deploy to correct.

### 2. Registry entries pointed at private repositories

Orphaned public metadata: `io.github.atomadictech/aaaa-nexus` and all 41 versions of `io.github.atomadictech/atomadic-forge` listed source repositories that 404 for the public. Repointed `aaaa-nexus` at `github.com/atomadictech/atomadic-mcp` and deprecated the forge entry with a pointer to the live server.
