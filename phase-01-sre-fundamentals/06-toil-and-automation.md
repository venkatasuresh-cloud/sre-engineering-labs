# Lesson 6 — Toil and Automation

**Toil** is operational work that tends to be manual, repetitive, automatable, reactive, and lacking enduring value. Not all manual work is toil.

## Examples

- **Toil:** Manually checking 50 application servers every morning.
- **Engineering:** Creating alerting that surfaces meaningful failures automatically.
- **Not necessarily toil:** Investigating a novel RDS performance incident that requires judgment.

## Caution: automating symptoms

A scheduled daily restart may reduce human effort but leave an application memory leak unresolved. Investigate recurring failures and fix causes; use automation for safe, well-tested operational workflows and recovery where appropriate.

For production automation, include guardrails, observability, approval requirements, rollback, and failure handling.
