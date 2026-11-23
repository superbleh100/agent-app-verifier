---
name: review-agent-app
description: Review an AI-first app (agents, workflows, skills, tools, MCP servers, sub-agents, memory) against docs/standards. Use when asked to review, audit or critique an AI app or its design, or whether each AI building block is the right one.
---

# Review an AI-first app

You are reviewing the *design* of a system built from AI building blocks: agents, workflows, LLM calls, skills, tools, MCP servers, sub-agents, code execution, memory and hooks. You're not linting code. Judge it only against `docs/standards/`, and cite a rule ID (BB-xx, AP-xx, SG-xx, ASIxx) for every finding. If something matters but no rule covers it, list it under "Gaps in the standards", not as a finding.

## Inputs

A repo path, a design doc, or a description. If there's no design doc, build one from the code first.

## Steps

1. **Load the standards.** Read every file in `docs/standards/`. Note any source in the registry whose "Last checked" date is more than 90 days old, and say so at the top of the report.
2. **Map the system.** Produce a component inventory and label every piece with its block type from `building-blocks.md`: code, LLM call, workflow, agent, sub-agent, tool, MCP server, skill, code execution, memory, hook or policy. For agents, record role, model, tools, permissions and memory. For skills and MCP servers, record what they expose and who uses them. Draw the control flow as a Mermaid diagram.
3. **Block-choice review (most important).** For every component, ask whether it is the right *kind* of block (BB-01 to BB-05). Is know-how hidden in a tool, or an action dressed up as a skill? Is a hard rule living only in a prompt? Is MCP used where a plain function would do? Is bulk data flowing through the model? Then, for every agent, answer these questions:
   - Can the steps be known in advance? If so, it should be a workflow or code (AP-02, AP-03).
   - Which named pattern is it, and is that the right one (the pattern table)?
   - Would a single LLM call or plain code do the job (AP-01, AP-04)?
   - Is its scope narrow, and does it overlap with another agent (AP-07, AP-08)?
   - **Multi-agent justification:** any design with more than one agent must name which AP-21 reason applies, or that's a finding. Also check AP-22 to AP-26.
   Also look for the reverse: brittle hard-coded logic that would be better as an agent.
4. **Block design review.** Skills: BB-06 to BB-11 (frontmatter, trigger description, progressive disclosure, scripts, provenance). Tools and MCP servers: BB-12 to BB-18 and AP-11 to AP-15. Context: AP-16 to AP-19. Runtime: BB-19 to BB-22. Also check stop conditions (AP-06).
5. **Security and governance review.** Go through ASI01–ASI10 and SG-01 to SG-20. Mark each as Met, Partial, Missing, or N/A, with evidence (a file:line or a doc section).
6. **Tooling review.** Compare what the app uses against `protocols-tooling.md`. Flag Experimental tech used in critical paths, and Settled options that the app reinvents.
7. **Write the report** to `reviews/<app>-<YYYY-MM-DD>.md`.

## Report format

```
# Review: <app> (<date>)
Standards version: <git short SHA of docs/standards or date>
## Summary: 3–5 sentences, top 3 actions
## System map (mermaid)
## Findings (ranked)
| # | Severity (High/Med/Low) | Rule | Finding | Evidence | Recommendation |
## Block-choice verdicts
| Component | Current block | Recommended block | Rule |
## Security/governance checklist (ASI + SG table)
## Gaps in the standards (things to add to docs/standards)
```

## Rules for yourself

- Severity: **High** means security exposure, an irreversible action without a gate, an agent where code would clearly do, or a hard rule enforced only by a prompt. **Med** means a wrong pattern or missing evals or observability. **Low** means hygiene.
- Rules marked *provisional* (resting only on T3 sources) can be at most Med severity.
- Don't recommend a specific vendor unless the standards library names it.
- Be concrete: every recommendation should be something a developer can act on.
