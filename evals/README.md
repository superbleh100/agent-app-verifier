# Self-test fixtures

Small sample apps with **known, labelled flaws**. `refresh-standards` runs `review-agent-app` on each one to check that the reviewer still catches what it should, and doesn't invent problems that aren't there.

Each fixture has:
- `design.md`: the app as a developer would describe it (plus a few code or config files)
- `expected.md`: the planted flaws with rule IDs and minimum severity, and things that must **not** be flagged

## Scoring

For each fixture, the reviewer's report is compared to `expected.md`:

- **Recall:** planted flaws found, with the right rule family, at or above the minimum severity
- **False alarms:** items under "must not flag" that were reported anyway
- **Precision note:** other findings are allowed, but are listed for a person to judge

Record each run in `evals/results/<YYYY-MM-DD>.md` as a table of fixture, recall, false alarms and notes.
A standards change that lowers recall on any fixture needs a written reason or gets dropped.

| Fixture | What it tests |
|---|---|
| 01-support-triage | An agent that should be a workflow, rules enforced only in prompts, too many endpoint-wrapper tools, no evals or logs |
| 02-research-assistant | A skill misused as an action, a secret inside a skill, MCP used without need, bulk data through context, memory poisoning, delegation that widens permissions |
| 03-invoice-extractor | **Control:** a well-built workflow. Tests for false alarms |
