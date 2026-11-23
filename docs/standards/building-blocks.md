# AI building blocks: choosing the right one

An AI-first app is built from several kinds of block, and "agent" is only one of them. The reviewer's first job is to check that each piece of the app uses the *right kind* of block. Rule IDs are BB-xx.

## The blocks

| Block | What it is | Use it when | Don't use it when |
|---|---|---|---|
| **Plain code** | Deterministic logic | The rule can be written down | — (it's the default) |
| **Single LLM call** | One prompt in, one answer out, maybe with retrieval or examples | Judgment or language work in a single step | Several dependent steps are needed |
| **Workflow** | LLM calls along code paths you define (chaining, routing, parallel, evaluator loop) | The steps are known in advance | The order of steps depends on what's found along the way |
| **Agent** | An LLM using tools in a loop and choosing its own steps | Open-ended work where the number of steps is unknown | Any of the blocks above would do |
| **Sub-agent** | An agent with its own clean context, called by a lead agent, that returns a short summary | Parallel or isolated research and analysis | The task is small, or needs the lead's full context |
| **Tool** | A function the model can call to act or fetch | An action or lookup the model needs | It just mirrors a raw API endpoint |
| **MCP server** | Tools, resources and prompts behind the open MCP protocol | Tools shared across apps, agents or clients | A single app needs one private function |
| **Skill** | A folder with SKILL.md, plus scripts and references, loaded only when relevant | Know-how about a procedure, domain or house style that the model should apply | It's really an action (use a tool) or always-on rules (use the system prompt) |
| **Code execution** | The model writes and runs code in a sandbox | Bulk data, filtering, loops, or calling many tools as code | No safe sandbox is available |
| **Memory / notes** | State kept outside the context window | Long-running or multi-session work | Plain chat history is enough |
| **Hooks / policy layer** | Code that runs before or after model actions | Rules that must *always* hold (permissions, approvals, formatting) | — (never put hard rules only in a prompt) |

Rules for choosing:

- **BB-01 Climb the ladder only as far as needed:** code → single call → workflow → agent → multi-agent. Every step up must be justified by measured gains. When an agent is warranted, a single agent with tools is the default rung (AP-21). [S1, S5, S14, S15]
- **BB-02 Actions are tools, know-how is skills.** "How to do X well" belongs in a skill. "Do X" belongs in a tool. Skills can teach the model how to use MCP tools. [S9]
- **BB-03 Hard guarantees are code or hooks, never just prompt text.** [S4, S5]
- **BB-04 Use MCP for reuse, not by reflex.** A tool used by one app can be a plain function. [S7, S11] *(T2)*
- **BB-05 Move bulk data to code execution.** If big intermediate results pass through the model, switch to code execution or filter before the model sees them. [S11]

## Skills [S9]

- **BB-06 Valid format:** a `SKILL.md` with YAML frontmatter `name` and `description`. Agent Skills is an open standard (agentskills.io).
- **BB-07 The description is the trigger.** Only the name and description are always loaded, so they must say clearly *when* to use the skill.
- **BB-08 Progressive disclosure.** Keep SKILL.md focused, put detail in linked files that are read only when needed, and keep paths that exclude each other separate.
- **BB-09 Scripts for deterministic steps.** Bundle code for anything that should be exact or repeatable. Say whether each script should be *run* or *read*.
- **BB-10 Built from evals.** Write a skill for gaps seen in real tasks, then iterate on transcripts.
- **BB-11 Supply-chain hygiene.** Skills come only from trusted sources. Audit bundled scripts and any instruction that reaches the network (see ASI04).

## Tools and MCP servers [S10, S11]

- **BB-12 Few tools that do whole jobs.** Combine multi-step chains into one tool (`schedule_event`, not list_users + list_events + create_event). Don't wrap every endpoint.
- **BB-13 Namespaced, unambiguous names**, such as `service_resource_action`, with input names like `user_id` rather than `user`.
- **BB-14 High-signal responses.** Return meaningful fields rather than raw IDs, offer a concise/detailed option, and paginate, filter or truncate with sensible defaults.
- **BB-15 Actionable errors** that tell the model what to try next, not stack traces.
- **BB-16 Strict schemas and annotations.** Flag destructive or open-world tools with MCP annotations so policy can gate them (SG-04).
- **BB-17 Don't load every tool up front.** For large tool sets, use tool search or a code-API layout so definitions load only when needed.
- **BB-18 Tools are evaluated.** Use realistic multi-step tasks with verifiable outcomes, and track accuracy, tool calls, tokens and errors on a held-out set.

## Runtime and hosting [S12]

- **BB-19 Stateless harness, durable session log.** The agent loop should be able to crash and resume from an append-only event log.
- **BB-20 Disposable sandboxes, provisioned on demand**, where a failed container just becomes a retryable tool error.
- **BB-21 Credentials never in the sandbox.** Use a vault or proxy, so the model's environment can't read secrets.
- **BB-22 Revisit harness workarounds when models change.** Workarounds for old model limits (such as context resets) can become dead weight.
