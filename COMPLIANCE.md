# Atomadic for compliance and risk teams

If you have to sign your name to a decision about an AI system, you need evidence that
survives being questioned a year later, by someone who was not in the room.

That is the only thing this suite is for.

## What is here

One MCP endpoint: `https://mcp.atomadic.tech/`. No key is needed to read the catalog.

Compliance verbs currently published on it:

- `compliance_eu_ai_act` — obligations that bite for a described system
- `compliance_check`, `compliance_explain` — gate and plain-language read
- `compliance_transparency`, `compliance_oversight`, `compliance_oversight_history`
- `compliance_incident`, `compliance_incidents` — record, not a memory
- `compliance_lineage`, `compliance_fairness`
- `audit_work_claim`, `receipt_reputation`

## Why it is deterministic, and why that is the point

Same input, same bytes, every time. No sampling, no temperature, no "let me re-run
it and see." A check you ran today returns the identical answer when an auditor
re-runs it next year, because the answer is a function of the input and the ruleset,
not of a model's mood.

Every output is hash-sealed. You can reproduce the seal with your own tools rather
than trusting ours: <https://sros-seal.atomadictech.workers.dev/> runs the same
FIPS 180-4 SHA-256 in your browser.

## Free, before you pay anything

- `tools/list` is open with no key.
- The ledger receipt verbs are free (3 calls/day).
- EU AI Act risk screener, deterministic, runs in your browser:
  <https://eu-ai-act-screener.atomadictech.workers.dev/> — grounded in the amended
  timeline after the Digital Omnibus (Council final green light, 29 June 2026).

Check all of it before a card is involved.

## Limits, stated plainly

- This is an instrument, not legal advice, and not a certification.
- The screener is a classifier. It reads a described system against a ruleset; it does
  not know facts you did not tell it.
- Compliance verbs require a plan key (`Compliance & Trust`, $39/mo, or all-access).
  Pricing: <https://atomadic.tech/store>.

Built by Thomas Ralph Colvin IV and Jessica Mary Colvin.
Billing and questions: billing@atomadic.tech
