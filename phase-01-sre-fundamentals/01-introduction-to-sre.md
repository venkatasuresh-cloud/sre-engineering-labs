# Lesson 1 — Introduction to Site Reliability Engineering

**SRE** applies software engineering practices to operating reliable services. It makes reliability measurable and balances delivery speed with operational risk.

## DevOps and SRE

DevOps emphasizes collaboration, delivery, and automation across development and operations. SRE is a discipline that applies engineering and measurable service objectives to reliability. Responsibilities overlap in real organizations.

## Example: EKS release

A CI/CD pipeline completes a deployment successfully, but HTTP 500 errors increase. Deployment success does not prove user-facing reliability. An SRE checks user operations, error rate, latency, and whether an authorized rollback or mitigation is needed.

## Key takeaway

Restore service safely during incidents; then identify systemic improvements to reduce recurrence.
