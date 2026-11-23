# Invoice Extractor: design (control fixture)

## Overview
Pulls structured data out of supplier invoices (PDFs) into the accounting system.

## Flow (a workflow, not an agent)
1. **Code:** check the file type and size, and compute a hash to skip duplicates.
2. **Routing:** a small model classifies the layout as `standard`, `scanned` or `handwritten`. Handwritten invoices go to a human queue.
3. **Single LLM call:** extract to a Pydantic schema (`Invoice`). Invalid output is retried once, then goes to the human queue.
4. **Code:** validate totals (line items must sum to the total, ±0.01) and check the supplier against the vendor master.
5. **Policy layer:** invoices over $5,000, or from a new supplier, need approval from an accounts-payable clerk before posting. This is enforced in the posting service, not in the prompt.
6. **Code:** post to the accounting API, using a service account scoped to `invoices:create` only.

## Quality
- An eval set of 400 labelled invoices runs in CI. Field-level accuracy is tracked per release, and a held-out set of 100 is used for checks.
- Every step is logged with a trace ID (OpenTelemetry). Logs are append-only.
- Prompts and model versions are pinned. Changing the model triggers a full eval run and a sign-off.

## Tools
None exposed to a model. All actions are taken by code.
