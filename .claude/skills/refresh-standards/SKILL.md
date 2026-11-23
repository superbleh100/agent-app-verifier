---
name: refresh-standards
description: Research the latest standards for AI-first apps (agents, skills, MCP, tools, evals, security), and propose updates to docs/standards and to the reviewer's own skill. Use when asked to refresh, update or self-evaluate the verifier.
---

# Refresh the standards (self-update loop)

The goal is to keep `docs/standards/` and `review-agent-app` current, without letting unverified hype in. **Never apply changes directly.** Make a branch and a PR, or a proposal file, for a person to approve.

## Steps

1. **Re-check known sources.** For each source in the registry in `docs/standards/README.md`, check for a newer version (for example a new OWASP list, an IMDA version, or Anthropic guidance). Update "Last checked".
2. **Scan for what's new since the last refresh.** Search these at minimum:
   - Standards bodies and governments: OWASP GenAI, NIST, ISO/IEC, IMDA, EU AI Office, W3C, Linux Foundation (A2A, AGNTCY)
   - Model vendors' engineering blogs (Anthropic, OpenAI, Google, Microsoft, AWS)
   - Vendor architecture guides re-checked every refresh: OpenAI practical guide (S13), Microsoft orchestration patterns (S14), Google design-pattern guide (S15), NIST CAISI (S16)
   - Protocol and format specs: MCP (spec changelog), A2A, WebMCP, Agent Skills (agentskills.io), AGENTS.md
   - New *kinds* of building block. If something new appears (a new extension type or runtime primitive), propose adding a row to the block table in `building-blocks.md`.
   - Open Known Gaps in the README
3. **Verify before adding anything.** Rate each candidate T1, T2 or T3 (see the README). A new rule needs one T1 source, or two independent T2 sources. Anything weaker is added as *provisional*, or put on a watch list. Also record adoption evidence: production users, spec version, and how many independent sources agree.
4. **Write a proposal** at `docs/proposals/refresh-<YYYY-MM-DD>.md` with these sections:
   - New rules (proposed ID, text, sources, tier)
   - Changed rules (the old text and the new text, and why)
   - Retired rules (superseded, with the evidence)
   - Maturity changes in `protocols-tooling.md`
   - Proposed changes to the `review-agent-app` skill itself
5. **Self-evaluate.** Run `review-agent-app` with the proposed standards against every fixture in `evals/fixtures/` (sample apps with known, labelled flaws in `expected.md`). Report what it caught and what it missed, before and after the change. A change that loses a previously caught flaw has to be justified or dropped. If there are no fixtures yet, say so and propose one.
6. **Open the change for approval.** Put the proposal and the diffs to `docs/standards/` on a branch and open a PR. Summarize the top changes in 5 bullets.

## Rules for yourself

- Prefer primary documents over blog summaries of them.
- Popularity isn't proof. Record *how* something was verified (spec, benchmark, real adoption), not just that people talk about it.
- Keep rule IDs stable. Retire a rule rather than renumbering.
