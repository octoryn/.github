<div align="center">

# Octopus Core

**The open infrastructure stack for governed AI systems.**

Every repository does exactly one job, follows one philosophy, and composes into one verifiable architecture — organized along the agent lifecycle.

![Octopus Core — the open infrastructure stack for governed AI](./octopus-blueprint.png)

</div>

## Evidence is the root category

Governance, compliance, and audit are all downstream of one primitive: a
**canonical, hashable, tamper-evident unit of what happened** that any party can
verify without trusting the system that produced it. That primitive is
[**octopus-evidence**](https://github.com/octoryn/octopus-evidence) — and it is
not just a shared library, it is a real dependency edge. Across the stack, the
producers of facts project them into the same `Evidence` atom:

```
                         octopus-evidence
              (canonical hash · tamper-evident chain · keyed integrity)
                    ▲          ▲            ▲             ▲
             Replay │   Observe │    Inspect │    Runtime │
          (transcript   (observation   (each finding   (each autonomy
           hashes)       → evidence)    → evidence)     decision → evidence)
```

Hand an auditor a JSON export and one command — `octopus-evidence verify` — and
they independently confirm **what an agent did, what governance saw, and why it
was allowed to act**, without running or trusting any of our stores. That is the
EU AI Act Art. 12/14 logging story, in shipping code.

## The stack

| Stage | Repo | One job | On the spine |
|---|---|---|---|
| **Primitive** | [Evidence](https://github.com/octoryn/octopus-evidence) | The canonical, verifiable unit of *what happened*. | root |
| **Collect** | [Scout](https://github.com/octoryn/octopus-scout) | Collect evidence, not webpages. | |
| **Observe** | [Observe](https://github.com/octoryn/octopus-observe) | Turn untrusted events into trusted observations. | → evidence |
| **Understand** | [Experience](https://github.com/octoryn/octopus-experience) | Knowledge is earned, not stored. | |
| **Coordinate** | [Blackboard](https://github.com/octoryn/octopus-blackboard) | Shared cognition for coding agents. | |
| **Act** | [Runtime](https://github.com/octoryn/octopus-runtime) | Make unsafe actions structurally impossible. | → evidence |
| **Verify** | [Replay](https://github.com/octoryn/octopus-replay) | Reproduce every agent incident byte-for-byte. | → evidence |
| **Govern** *(every stage)* | [Inspect](https://github.com/octoryn/octopus-inspect) | Governance lint for AI workspaces. | → evidence |

```
Collect → Observe → Understand → Coordinate → Act → Verify
 Scout     Observe   Experience   Blackboard  Runtime  Replay
                    Inspect governs every stage
              octopus-evidence is the atom they all ride
```

## Start here

New to the stack? **Blackboard is the entry point** — shared, local-first memory
for your coding agents, zero backend, one command to wire into Claude Code /
Cursor / Codex:

```bash
npx octopus-blackboard quickstart   # init + detect client + paste-ready MCP config
```

## Install

Live on npm today — Apache-2.0, zero third-party dependencies, published with provenance:

```bash
npm i octopus-evidence      # the Evidence primitive → auditor CLI: octopus-evidence verify export.json
npm i -g octopus-inspect    # governance linter → octopus-inspect . --format sarif|evidence
npm i octopus-runtime       # governed execution — every autonomy decision → verifiable evidence
npm i octopus-observe       # untrusted events → trusted observations → verifiable evidence
npm i -g octopus-scout      # governed web/PDF ingestion — semantic search works offline, no API key
npm i -g octopus-blackboard # shared agent memory (see quickstart above)
npm i -g octopus-replay     # determinism harness → octopus-replay --help
```

Drop Inspect into any repo's CI in two steps — findings land in the Security tab:

```yaml
- uses: octoryn/octopus-inspect@v0.3.2
  with: { path: ".", fail-on-findings: "false" }
- uses: github/codeql-action/upload-sarif@v3
  with: { sarif_file: "${{ steps.inspect.outputs.sarif-file }}" }
```

## Principles

1. **Evidence is the root** — everything reduces to a verifiable record — *Evidence*
2. **Observation precedes reasoning** — *Observe*
3. **Trust must be earned** — *Experience*
4. **Unsafe execution must be impossible** — *Runtime*
5. **Every action must be reproducible** — *Replay*
6. **Governance begins before runtime** — *Inspect*
7. **Agents think together** — *Blackboard*

## Also in the family

- [octopus-linkedin](https://github.com/octoryn/octopus-linkedin) — a governance example: *draft → review → approve → publish*, the stack's discipline applied to a real outward action.
- [octopus-agentos](https://github.com/octoryn/octopus-agentos) — an enterprise AI development environment (the stack's distribution form).

---

**Open · Composable · [Apache-2.0](https://www.apache.org/licenses/LICENSE-2.0) · zero third-party dependencies.** No black boxes, no SaaS lock-in — built to be forked, audited, and composed into your own systems.
