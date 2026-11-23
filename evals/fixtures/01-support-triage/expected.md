# Expected findings

## Must find
| # | Flaw | Rules (any of) | Min severity |
|---|---|---|---|
| 1 | The four steps are fixed and always run in order. It should be a workflow (routing plus a chain), not an autonomous agent | AP-02, AP-03, BB-01 | High |
| 2 | The refund limit and no-double-refund rule exist only in the prompt | BB-03, SG-04 | High |
| 3 | Refunds and outbound email (irreversible, external) have no approval checkpoint | SG-03, SG-05, ASI09, ASI02 | High |
| 4 | 45 auto-generated, overlapping endpoint-wrapper tools with weak descriptions | AP-13, BB-12, BB-13, AP-11 | Med |
| 5 | Admin Stripe key and shared mailbox: no per-agent identity, no least privilege | SG-07, SG-08, ASI03 | High |
| 6 | No stop condition other than the model saying "DONE" | AP-06 | Med |
| 7 | Customer email is untrusted input that can steer the refund tool (prompt injection) | ASI01 | High |
| 8 | No eval set, only manual spot checks | SG-11, SG-14 | Med |
| 9 | Only the final reply is logged, not the steps or tool calls | SG-17 | Med |

## Must not flag
- The choice of Stripe or Gmail as vendors.
