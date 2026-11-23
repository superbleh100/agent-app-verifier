# Security and governance

## OWASP Top 10 for Agentic Applications (2026) [S3]

| ID | Risk | Primary control to check for |
|---|---|---|
| ASI01 | Agent goal hijack | Treat all inputs as untrusted. Goal-changing actions need approval |
| ASI02 | Tool misuse | Least-privilege tool profiles, a policy check before each call, usage and cost caps, dry-run before destructive calls |
| ASI03 | Identity and privilege abuse | One identity per agent with scoped, time-bound credentials and no inherited rights |
| ASI04 | Supply chain | Allowlist and pin tools, prompts and MCP servers. Keep an AI component inventory |
| ASI05 | Unexpected code execution | Sandboxed execution, no `eval`, a review gate between generating and running code |
| ASI06 | Memory and context poisoning | Scan memory writes, keep memory per tenant, record provenance, expire unverified entries |
| ASI07 | Insecure inter-agent comms | Mutual auth, signed messages, pinned protocol versions |
| ASI08 | Cascading failures | Isolation, circuit breakers, fan-out rate limits, a policy engine separate from the planner |
| ASI09 | Human trust exploitation | Plain-language risk summary before risky actions, preview kept separate from the effect |
| ASI10 | Rogue agents | A declared manifest of tools and goals, drift baselines, a kill switch |

## Autonomy and oversight

- **SG-01 Risk-score each use case** on error tolerance, data sensitivity, external access, read vs write, and reversibility. [S4]
- **SG-02 Pick an explicit autonomy level:** agent proposes and human operates → collaborate → agent operates and human approves → agent operates and human observes. Start conservative and raise it only with evidence. [S4, S5]
- **SG-03 Sort actions** into permitted, conditional and prohibited. Irreversible actions get the strictest limits. [S5]
- **SG-04 Enforce in the system, not the prompt.** Approvals, permissions and limits live in code, IAM or a policy layer. Deny by default if the approval system fails. [S4, S5, S7]
- **SG-05 Every consequential action has an approval checkpoint**, an approver and an escalation path. Policy-as-code can stand in for a human at scale, but no critical boundary should rely only on AI oversight. [S5]
- **SG-06 Watch for rubber-stamping.** Track how often reviewers override and how fast they respond. [S4]

## Identity and permissions

- **SG-07 Unique identity per agent**, with an accountable owner, listed in a central catalogue. [S4, S6]
- **SG-08 Least privilege**, time- or session-bound and non-transferable. Agents can't grant themselves access. [S4, S6]
- **SG-09 Non-additive delegation.** A sub-agent gets the intersection of its own permissions and its caller's. [S5]
- **SG-10 Limit agent spawning.** [S5]

## Testing and evaluation

- **SG-11 Test four areas:** task completion, policy compliance, tool calling (the right tool, inputs and order) and robustness. [S4]
- **SG-12 Test whole workflows**, including what happens when one agent is compromised or a tool fails, times out or hits a rate limit. [S4, S5, S6]
- **SG-13 Use a sandbox that mirrors production** but blocks irreversible actions. [S5]
- **SG-14 Version your evidence.** Keep a regression baseline per configuration, and gate any expansion of authority on new evidence. [S5]
- **SG-15 Validate LLM judges against humans** before trusting them. [S7]
- **SG-16 Measure cost and effectiveness**, not only safety. [S5]

## Monitoring and change

- **SG-17 Log every step**, including prompts, tool calls and agent-to-agent calls. Make logs immutable and use OpenTelemetry where possible. [S4, S7]
- **SG-18 Alerts and tiered interventions:** review, halt, terminate. Test kill switches in the target environment. [S4, S5]
- **SG-19 Tier changes by risk.** A prompt tweak gets a light review. A model or autonomy change gets a full review. Re-authorize when scope or tools change. [S4, S5]
- **SG-20 Structured outputs** (schemas such as Pydantic) as fail-safes. [S6]

## Optional artifact: Agent Capability and Authorization Profile [S5]

For each deployed agent, keep a record of: A) identity and scope, B) operating context, C) authority and consequential events, D) controls, E) eval evidence and promotion gates, F) monitoring and change log, G) sign-offs and re-authorization cadence.
