# Architecture patterns

Rule IDs (AP-xx) are what review reports cite.

## Does this need an agent? (the most important question)

- **AP-01 Simplest thing first.** Try a single well-prompted LLM call with retrieval and examples first, then a workflow, and only then an agent. Add complexity only when it measurably improves outcomes. [S1, S2]
- **AP-02 Workflow vs agent.** A *workflow* runs LLM calls along code paths you defined. An *agent* decides its own steps and tool use in a loop. Use an agent only when the number or order of steps can't be known in advance. [S1]
- **AP-03 Pre-scripted is not an agent.** If every step is fixed, it's automation. Writing it as an agent adds cost, latency and unpredictability for nothing. [S5]
- **AP-04 Deterministic where possible.** Keep logic that can be coded (validation, routing on known fields, math, formatting) in code, not in the LLM. [S4, S7]

## Named patterns and when they fit [S1]

| Pattern | Fits when | Watch for |
|---|---|---|
| Prompt chaining | Task splits into fixed sequential steps | Add code "gates" between steps |
| Routing | Inputs fall into distinct categories that classify reliably | Route easy cases to a cheaper model |
| Parallelization (sectioning / voting) | Independent subtasks, or you need confidence from multiple tries | Merge logic must be explicit |
| Orchestrator-workers | Subtasks can't be predicted up front | Workers need clean, scoped context |
| Evaluator-optimizer | Clear criteria exist and feedback measurably improves output | Cap the iterations |
| Autonomous agent | Open-ended, step count unknown, environment gives ground truth | Needs stop conditions, sandboxing, human checkpoints |

- **AP-05 Ground truth each step.** Agents should check real results (tool output, tests, execution), not just their own reasoning. [S1]
- **AP-06 Stop conditions.** Every loop has a max iteration count or budget, plus a path to pause for a human when it's stuck. [S1]
- **AP-07 Narrow agents.** Give each agent one clear role with a minimal scope. Avoid an "all-powerful" single agent. [S4, S6]
- **AP-08 No duplicated responsibility.** Map which agent owns each task, the order they run in, and what depends on what. [S6]
- **AP-09 Structured inter-agent messages.** Agents talk to each other through schemas, not free text. [S4, S6]
- **AP-10 Sub-agents for clean context.** Use sub-agents for parallel research or analysis, returning condensed summaries (around 1–2k tokens) to a lead agent. [S2]

## Tool design (the agent-computer interface)

- **AP-11 Tools deserve as much design as UI.** Each tool needs a clear description, examples, edge cases and boundaries against the other tools. [S1]
- **AP-12 Poka-yoke tools.** Shape arguments so mistakes are hard to make (for example, require absolute paths). [S1]
- **AP-13 Minimal, non-overlapping tool set.** If a human couldn't say which tool to use, the model can't either. Boundaries blur at roughly 20–50 tools, so split into specialist agents beyond that. [S2, S7]
- **AP-14 Model-friendly formats.** Avoid formats that force counting or heavy escaping (for example, code inside JSON). [S1]
- **AP-15 Don't use MCP where a function call will do.** Use MCP when a tool is shared or reused, not by reflex. [S7] *(T2)*

## Context engineering [S2]

- **AP-16 Smallest high-signal context.** Context rot is real, and a bigger window doesn't fix pollution.
- **AP-17 Prompt "altitude".** Avoid both brittle if/else rules in prompts and vague guidance. Use sections, and add instructions only for failures you've actually seen.
- **AP-18 Just-in-time retrieval.** Pass identifiers (paths, links, queries) and load data through tools, rather than stuffing everything in up front. A hybrid approach is fine.
- **AP-19 Long-horizon strategy chosen on purpose:** compaction for long chats, structured notes or memory for milestone work, sub-agents for parallel work.

## Frameworks

- **AP-20 Know what the framework does.** Heavy abstractions hide prompts and responses. Start with direct API calls, or understand what runs underneath the framework. [S1]
