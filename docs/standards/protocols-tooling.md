# Protocols and tooling landscape

Maturity: **Settled** (safe default), **Emerging** (adopt with care), **Experimental** (watch only).
Mostly from S8 (T3), so these are *provisional* until checked against each protocol's own docs.

| Layer | Standard | Steward | Maturity | Use it for |
|---|---|---|---|---|
| Agent ↔ tools/data | MCP | Anthropic-led, open spec | Settled | Shared or reusable tools and data sources. Watch for context bloat and injection through tool descriptions |
| Agent ↔ agent | A2A (v1.0, Apr 2026; absorbed IBM ACP) | Linux Foundation | Emerging→Settled | Delegation between agents across teams or vendors, using Agent Cards |
| Website ↔ agent | WebMCP | Google + Microsoft via W3C | Experimental | Sites exposing actions to browser agents |
| Agent ↔ UI | AG-UI | Framework-led | Experimental | Streaming agent state to a front end |
| Semantics | OSI | Snowflake + partners, Apache 2.0 | Emerging | Shared business metric definitions |
| Payments | AP2, ACP, x402 | Various | Experimental | Agent spending. No clear winner yet |
| Identity | Signed Agent Cards, Web Bot Auth, MCP-I, DIDs | Fragmented | Experimental | Track only |
| Repo conventions | AGENTS.md, llms.txt | Community | Emerging | Instructions for coding agents |

## Not standardized yet

Reasoning and orchestration, evaluation and provenance, and agent traffic economics.

## Tooling categories the reviewer checks for (vendor-neutral)

- Agent SDK or framework, and whether its abstraction is justified (AP-20)
- An eval harness with a regression set (SG-11, SG-14)
- Tracing and observability, ideally OpenTelemetry (SG-17)
- Sandboxed code execution (ASI05)
- A policy or guardrail layer outside the prompt (SG-04)
- Memory store with provenance (ASI06)
