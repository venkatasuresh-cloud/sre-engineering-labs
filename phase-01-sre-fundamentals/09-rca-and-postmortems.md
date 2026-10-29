# Lesson 9 — RCA and Blameless Postmortems

## The distinction

- **Mitigation:** Restore or stabilize user-facing service.
- **RCA:** Establish supported underlying causes and contributing conditions.
- **Postmortem:** Record impact, timeline, actions, evidence, uncertainties, and follow-up improvements.

## Example chain

1. **Symptom:** Students see HTTP 500 on login.
2. **Immediate cause:** Application cannot acquire MySQL connections.
3. **Underlying cause (only if proven):** Application fails to return connections to the pool.
4. **Contributing factor:** Pre-production tests did not simulate the triggering usage pattern.

Restarting the application may mitigate the incident without completing RCA. A blameless postmortem examines which safeguards failed and how to strengthen them, rather than blaming an individual for introducing a bug.

## Template

- Summary and user impact
- Incident start/end and detection method
- Timestamped timeline
- What worked / what did not
- Confirmed causes, contributing factors, unknowns
- Mitigation and recovery validation
- Action items (owner, priority, due date, verification)

Never publish real customer or employer incident details without permission.
