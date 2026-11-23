# Agent App Verifier

An on-demand reviewer for **AI-first apps**: apps built from agents, workflows, skills, tools, MCP servers, sub-agents and memory. It comes with a standards library that it keeps up to date and tests itself against.

## Use it (Claude Code)

| Command | What it does |
|---|---|
| `/review-agent-app <repo path or design doc>` | Maps the app, checks that each part is the right kind of building block, and checks it against the standards. Writes a ranked report to `reviews/` |
| `/refresh-standards` | Researches new standards and tools, verifies them, re-runs the self-tests, and proposes the changes as a PR for you to approve |

## Layout

- `docs/standards/`: the standards library. Rules are numbered and sourced, with a trust tier and a last-checked date. Start at [docs/standards/README.md](docs/standards/README.md).
- `.claude/skills/`: the two skills above.
- `evals/fixtures/`: sample apps with known flaws, used for self-testing.
- `docs/proposals/`: refresh proposals waiting for review.
- `reviews/`: review reports.

## Principles

1. Every rule cites a source and records how it was verified.
2. The reviewer never changes its own rules without a person's approval.
3. A change that makes the reviewer miss a known flaw is rejected unless there's a written reason.
