# Escalation Policy

## Escalation Triggers

The conversation is escalated when:

- Authentication fails after 3 attempts
- Backend services are unavailable
- Tool execution fails
- Customer requests a human agent
- Business rules prevent automated resolution

---

## Context Transfer

The following information is transferred during escalation:

- customer_id
- selected_order_id
- active_intent
- conversation_summary

---

## Objective

Ensure seamless handoff to a human agent while minimizing customer effort and repetition.
