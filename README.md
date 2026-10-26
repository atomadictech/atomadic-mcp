# aaaa-nexus — public entry point

This repo is the public front page for the **AAAA-Nexus** hosted MCP server:
formally verified AI safety and compliance APIs, reachable over HTTP with no
signup.

The server is live. The source is not public. That is the whole point of this
repo: if you landed here from an MCP directory and every other Atomadic link
was a dead end, this is the one that resolves.

## Live endpoint

```
https://aaaa-nexus.atomadictech.workers.dev/mcp
```

Streamable HTTP, MCP protocol revision `2025-11-25`. Verified live:

```bash
curl -s -X POST https://aaaa-nexus.atomadictech.workers.dev/mcp \
  -H 'content-type: application/json' \
  -H 'accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"initialize","params":{"protocolVersion":"2025-06-18","capabilities":{},"clientInfo":{"name":"probe","version":"1"}}}'
```

Then `tools/list` and `tools/call`. 44 tools are exposed. A sample:

`rng_quantum`, `threat_score`, `hallucination_oracle`, `identity_verify`,
`ratchet_register`, `authorize_action`, `spending_authorize`, `lineage_record`.

The catalog also mirrors at
`https://aaaa-nexus.atomadictech.workers.dev/.well-known/mcp.json`.

## The 30-second proof (no key, no account)

The full catalog lives at `https://mcp.atomadic.tech` (129 tools; a key unlocks
your plan's set). Three tools need no key at all. Run this pair and you have
seen the thing work:

```bash
# 1. orientation: install, connect, what you are entitled to
curl -s -X POST https://mcp.atomadic.tech \
  -H 'content-type: application/json' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"murmuration","arguments":{}}}'

# 2. the proof: one function emitted into 12 languages from one source
curl -s -X POST https://mcp.atomadic.tech \
  -H 'content-type: application/json' \
  -d '{"jsonrpc":"2.0","id":2,"method":"tools/call","params":{"name":"render_polyglot_all_pure","arguments":{"atom_name":"compute_sum_pure"}}}'
```

That second call returns `ok: true` with Python, JavaScript, TypeScript, Rust,
Go, C#, Kotlin, Swift, Ruby, Lua, Elixir and Haskell, all from a single node IR.

The baked demo atoms are `compute_sum_pure`, `keep_positive_pure`,
`double_each_pure`, `count_words_pure`. Call the polyglot tools with an empty
argument and they answer, honestly, `novel_input_not_baked` — that is a
boundary, not a bug: arbitrary input is what the SDK is for.

Keys are sold at `https://atomadic.tech/store`. A key is emailed after checkout,
and `X-API-Key` or `Authorization: Bearer ato_<key>` is the whole auth story.

## How calls get paid

`tools/call` returns an invocation contract: an HTTPS URL, a method, and a price
in micro-USDC. Pay it with either

- **x402** — complete payment per `PAYMENT-REQUIRED` on the `402` from the
  target route, or from `/v1/payments/fee`, sending an `x402 PAYMENT-SIGNATURE`
  header; or
- **X-API-Key** — if you already hold a key.

No account is required for x402. Pay per call.

## Elsewhere

- `https://atomadic.tech` — main site, docs, pricing, proof page
- `https://aaaa-nexus.atomadictech.workers.dev` — the server itself

## On missing links

Some older pages and package metadata point at GitHub repositories that are
private. Those links 404 for anyone outside the account. Nothing was deleted;
the repositories are closed. If you followed a broken link to get here, this
README is the correction: use the live endpoint above rather than the dead
source link.

## Registry listing

Official MCP Registry entry: `io.github.atomadictech/aaaa-nexus` (latest
0.5.1), with `repository` pointing at this repo and the live remote above.
The older `io.github.atomadictech/atomadic-forge` entries are marked
**deprecated**: that endpoint returns 404 and its package is retired.

    https://registry.modelcontextprotocol.io/v0/servers?search=atomadic

Built by Thomas Ralph Colvin IV and Jessica Mary Colvin.
