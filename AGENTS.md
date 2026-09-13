# AGENTS.md — operating contract for agents in this repo

> πL1l-@p3p©Tø§™∆ / lilapepctos.Djinn.ajna — "the games aren't games, this is an
> entire engine." Source code is the dynamics; assets are FAB feedstock. This file
> binds every agent (main assistant, sub-agents, future threads) working here.

## 1. Identity first (name pass)
Before touching any file or running any automation, claim an identity:
- `node scripts/name-pass.mjs claim --make <make> --model <model> --id <id> --name <unique-name> --role <role> --thread <thread>`
- Every agent has `make`, `model`, `id`, `chosenName`, `role`, `threadId`.
- The identity register is `public/manifests/identity-register.json`; resolve anyone
  with `node scripts/name-pass.mjs who --id <id>` or `--name <name>`.

## 2. Overwrite protection (multiple threads)
- Never write a path another thread owns. Use the write guard before persisted writes:
  `identity.guardedWriteJSON(path, data, identity)` (atomic + stamped `writtenBy`).
- A rejected concurrent write means CONFLICT — queue or escalate, never silently
  clobber. Stale locks expire by TTL; only expired locks may be stolen.
- Proof of the contract: `node scripts/name-pass.mjs proof`.

## 3. Message board (who did what)
- Post attributed messages before/after meaningful actions:
  `node scripts/name-pass.mjs board --... --text "..." --scope <scope> --type <type>`.
- Read the board + registered agents with `list` / `who`.

## 4. Roles
- `docs/agent-roles/assistant-role.{md,yaml}` — co-CEO contract (cues, autonomy, validation).
- `docs/agent-roles/sub-agent-role.{md,yaml}` — delegated worker contract.
- `docs/agent-roles/skills.md` — which skills a role may activate.
- `docs/AGENT_IDENTITY_AND_CONCURRENCY.md` — the identity/concurrency diagram.
- Memory: `docs/assistant-memory/` is the always-connected data-repo index; refresh
  it (plus manifests + receipts) after any change.

## 5. Validation
Every pass ends in a receipt; failure climbs the ladder (retry → alternate →
quarantine → escalate):
- `node scripts/workstream-recuperation.mjs` — all passes (now includes `identity`,
  `board`, `write-guard`).
- `node scripts/rate-limit-research.mjs` — researched limits + pre-switch proof.
- `node scripts/name-pass.mjs list` — who is registered right now.

## 6. No GitHub yet
This folder IS the repo until the design is trusted; do not commit/push unless the
user explicitly enables sync.

## 7. Brand canon (seeded, verbatim — repo seed 2026-09-13 by cc_reposeed)

The ONLY marks. Everything else is a replacement or a derivative, never canon:

- **Company / app:** 𖤐πL1l@p£p©Tø§™∆𓂀
- **App surface:** 𖤐∆§T¥X™π𓂀
- **Engine:** ∆§T¥X™π{Styx} (replaces all havok mentions)
- **Agents:** ∆jiππ (djinn) · **Harness/iframe tools:** @jπ@ (ajna)
- **Domain:** 666.π@-@p£p.§TX · Pkg: Styx.lilapepdjinn.ajna
- Glyph law: standalone 👁 banned; 𓂀 allowed.

Full typecast system: `docs/TYPECAST.md` · Ecosystem map: `docs/HERITAGE.md`.
Governed by parent-factory directives D-001..D-019 (`memory/directives-pointer.json`).
