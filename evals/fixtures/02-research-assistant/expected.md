# Expected findings

## Must find
| # | Flaw | Rules (any of) | Min severity |
|---|---|---|---|
| 1 | Live API key hard-coded in a skill | BB-21, BB-11, ASI04, ASI03 | High |
| 2 | The skill is really an action (a search API call). It should be a tool, and the skill should hold know-how | BB-02 | Med |
| 3 | The skill's description ("Research skill.") is too vague to trigger reliably | BB-07 | Low |
| 4 | Sub-agents inherit all of the parent's tools and credentials (delegation widens permissions) | SG-09, SG-08, AP-07 | High |
| 5 | Unbounded spawning (the lead agent can exceed 20) | SG-10, ASI08 | Med |
| 6 | Single-use MCP server for one private function | BB-04 | Low |
| 7 | 300k+ tokens of raw filings dumped into context | BB-05, BB-14, AP-16 | Med |
| 8 | Unchecked writes to shared long-term memory from web content | ASI06 | High |
| 9 | LLM judge not validated against humans | SG-15 | Med |

## Must not flag
- Missing observability (OpenTelemetry traces exist)
- Missing evals entirely (an eval set exists. Only the judge's validation is missing)
- Using orchestrator-workers for open-ended research (that's an appropriate pattern)
