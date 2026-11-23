# Research Assistant: design

## Overview
An internal assistant that writes market-research briefs. A lead agent plans the work and spawns sub-agents.

## Components
- **Lead agent**: plans and spawns up to 20 `researcher` sub-agents per request. It can spawn more if it decides to.
- **Researcher sub-agents**: inherit *all* of the lead agent's tools and credentials, including `write_crm` and `send_slack`.
- **`web-research` skill**: see `skills/web-research/SKILL.md`.
- **`company-db` MCP server**: written for this app only. It exposes a single tool, `lookup_company(name)`, and nothing else uses it.
- **`export_all_filings` tool**: returns every SEC filing for a company as raw text (often 300k+ tokens) straight into the model's context, which then picks out the numbers.
- **Long-term memory**: researchers save "useful facts" from web pages into a shared vector store, which all future runs read. Writes aren't checked.

## Evaluation
We have 30 sample questions with expected briefs, scored by an LLM judge. The judge hasn't been compared with human ratings.

## Ops
Traces go to an OpenTelemetry collector.
