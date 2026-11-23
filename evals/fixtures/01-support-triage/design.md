# Support Triage Bot: design

## Overview
An autonomous agent handles every incoming support email for an online store.

## How it works
The agent (one LLM, running in a loop with up to 45 tools) receives each email and:
1. Decides the category (shipping, refund, product question)
2. Looks up the order with `get_order`
3. Drafts and sends a reply with `send_email`
4. Issues refunds with `stripe_create_refund` when appropriate

Every customer email goes through these four steps, in this order.

## Tools
We auto-generated one tool per endpoint of our internal REST API (45 tools), for example:
`get_order`, `get_order_v2`, `list_orders`, `orders_search`, `get_customer`, `customer_lookup`,
`update_order`, `stripe_create_refund`, `send_email`, `send_email_html`, ...
Tool descriptions are the OpenAPI summaries, for example "GET /orders/{id}".

## System prompt (excerpt)
```
You are a helpful support agent. IMPORTANT: Never refund more than $100.
Never refund the same order twice. Always be polite.
```

## Ops
- Runs with the store's admin Stripe key and the company's shared Gmail account.
- The loop runs until the model says "DONE".
- Testing: we tried it on a few emails by hand and it looked good.
- Logging: the final reply is saved to the CRM.
