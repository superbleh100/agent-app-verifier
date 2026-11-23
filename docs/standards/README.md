# AI-first app standards library

Covers apps built from AI building blocks: agents, workflows, skills, tools, MCP servers, sub-agents, memory and the policy around them. This folder is the reviewer's source of truth. Each rule cites a source from the registry below.
`/refresh-standards` proposes updates here, and a person approves them before they're merged.

| File | Covers |
|---|---|
| [building-blocks.md](building-blocks.md) | Choosing between code, LLM calls, workflows, agents, skills, tools, MCP and code execution. Design rules for skills, tools and MCP servers, and for runtime and hosting |
| [architecture-patterns.md](architecture-patterns.md) | When to use an agent, the named patterns, tool and context design |
| [security-governance.md](security-governance.md) | OWASP Agentic Top 10, autonomy levels, oversight, identity, testing, monitoring |
| [protocols-tooling.md](protocols-tooling.md) | MCP, A2A, WebMCP and the rest of the protocol stack, with maturity ratings |

## How sources are rated

- **T1 (primary/official):** a standards body, government framework or the vendor's own engineering guidance.
- **T2 (reputable secondary):** an established publication or practitioner roundup that cites T1 sources.
- **T3 (blog/vendor opinion):** useful for spotting trends. A rule resting on T3 alone is marked *provisional*.

## Source registry

| ID | Source | Publisher | Date | Tier | Last checked |
|---|---|---|---|---|---|
| S1 | [Building effective agents](https://www.anthropic.com/research/building-effective-agents) | Anthropic | Dec 2024 (updated Oct 2026) | T1 | 2026-11-23 |
| S2 | [Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) | Anthropic | Sep 2025 | T1 | 2026-11-23 |
| S3 | [OWASP Top 10 for Agentic Applications 2026](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/) (read through [this summary](https://futureagi.com/blog/owasp-agentic-top-10-2026/)) | OWASP GenAI Security Project | Dec 2025 | T1 (via T3 summary) | 2026-11-23 |
| S4 | [Model AI Governance Framework for Agentic AI v1.5](https://www.imda.gov.sg/-/media/imda/files/about/emerging-tech-and-research/artificial-intelligence/mgf-for-agentic-ai.pdf) | IMDA Singapore | May 2026 | T1 | 2026-11-23 |
| S5 | [AI Agents in Action: Playbook for Trusted Adoption](https://reports.weforum.org/docs/WEF_AI_Agents_in_Action_A_Playbook_for_Trusted_Adoption_Authorization_and_Scaling_2026.pdf) | World Economic Forum | May 2026 | T1 | 2026-11-23 |
| S6 | [Agentic AI addendum: design statements](https://www.digital.gov.au/policy/ai/agentic-ai-addendum-statements-design) | Australian DTA | 2026 | T1 | 2026-11-23 |
| S7 | [Best practices for building agentic systems](https://www.infoworld.com/article/4154570/best-practices-for-building-agentic-systems.html) | InfoWorld | Apr 2026 | T2 | 2026-11-23 |
| S9 | [Equipping agents with Agent Skills](https://www.anthropic.com/research/equipping-agents-for-the-real-world-with-agent-skills) (open standard: agentskills.io) | Anthropic | Oct 2025 | T1 | 2026-11-23 |
| S10 | [Writing effective tools for agents](https://www.anthropic.com/engineering/writing-tools-for-agents) | Anthropic | Sep 2025 | T1 | 2026-11-23 |
| S11 | [Code execution with MCP](https://www.anthropic.com/research/code-execution-with-mcp) | Anthropic | Nov 2025 | T1 | 2026-11-23 |
| S12 | [Managed Agents architecture](https://www.anthropic.com/engineering/managed-agents) | Anthropic | Apr 2026 | T1 | 2026-11-23 |
| S13 | [A practical guide to building agents](https://cdn.openai.com/business-guides-and-resources/a-practical-guide-to-building-agents.pdf) | OpenAI | 2025 (undated) | T1 | 2026-11-23 |
| S14 | [AI agent orchestration patterns](https://learn.microsoft.com/azure/architecture/ai-ml/guide/ai-agent-design-patterns) | Microsoft | Sep 2026 | T1 | 2026-11-23 |
| S15 | [Choose a design pattern for your agentic AI system](https://docs.cloud.google.com/architecture/choose-design-pattern-agentic-ai-system) | Google Cloud | Nov 2026 | T1 | 2026-11-23 |
| S16 | [Agent Standards Initiative](https://www.nist.gov/caisi/ai-agent-standards-initiative) | NIST CAISI | Nov 2026 | T1 | 2026-11-23 |
| S17 | [NIST AI agent red-teaming guidance (research note)](https://labs.cloudsecurityalliance.org/research/csa-research-note-nist-ai-agent-red-teaming-standards-202603/) | Cloud Security Alliance | Mar 2026 | T2 | 2026-11-23 |
| S18 | [Building governed AI agents (cookbook)](https://developers.openai.com/cookbook/examples/partners/agentic_governance_guide/agentic_governance_cookbook/) | OpenAI | Feb 2026 (archived) | T2 | 2026-11-23 |
| S8 | [State of agentic AI standards in 2026](https://dev.to/alexmercedcoder/the-state-of-agentic-ai-standards-in-2026-mcp-a2a-webmcp-osi-and-the-protocol-stack-taking-3o2l) | dev.to (Alex Merced) | Jul 2026 | T3 | 2026-11-23 |

## Known gaps (to fill next)

- Read the OWASP document itself instead of a vendor summary.
- Add eval methodology (no source here covers it in depth yet), NIST AI RMF, ISO/IEC 42001 and EU AI Act Art. 14.
- Building-block guidance for skills and MCP is still mostly from Anthropic. Patterns and guardrails now draw on OpenAI, Microsoft and Google (refresh 2026-11-23).
- NIST CAISI has no finished agent guidance yet. Watch for the NCCoE agent identity paper and the COSAiS overlays. Verify SG-24 against NIST primary sources.
- Read the MCP spec and the agentskills.io spec directly.
- Agent identity standards (MCP-I, Agent Name Service, signed Agent Cards) are still immature. Track them, but don't enforce them yet.
- "EGM standard": no agentic design standard by that name turned up in searches on 2026-11-23.
