# Principles: Operational Safety

## Human Error is a System Problem

In distributed systems, humans are both the greatest source of resilience and the most frequent trigger of failure. A fatigued engineer dropping a production table or an incident commander misdiagnosing a cascading failure aren't just "human errors"—they are systemic vulnerabilities.

## Designing for Safe Failure

The goal of operational safety isn't to prevent mistakes. That's impossible. The goal is to build systems that absorb mistakes without catastrophic consequences, providing technical and psychological safety nets.

## The Pillars of Operational Safety

1. **Automation as a Safety Net:** Automate repetitive, error-prone tasks (deployments, certificate rotation) to remove the opportunity for manual error. But for novel failures, keep humans in the loop. Automation should pause, alert, and hand control back safely when it encounters the unknown.
2. **Psychological Safety:** If engineers fear breaking production, they will hide mistakes, delay maintenance, and hesitate to escalate incidents. Blame destroys visibility. You can't fix systemic flaws if people are afraid to point them out.
3. **The Blast Radius Principle:** When a mistake happens, the impact must be contained. If a bad config can take down the global fleet, the architecture is unsafe. Stagger deployments, decouple databases, and use bulkheads to stop cascading failures.
4. **Defense in Depth:** Single points of failure are unacceptable in both infrastructure and process. A deployment pipeline needs automated tests (first defense), canary analysis (second defense), and a one-click rollback (third defense).

## Anti-Patterns

Ignoring operational safety results in extended downtime, toil, and attrition.

* **The "Fat Finger" Outage:** An engineer runs a destructive query in production instead of staging. Without guardrails—like default read-only access, peer review for production DB execution, or point-in-time recovery—the business loses data.
* **Burnout by Design:** Paging engineers for noisy, non-actionable alerts and expecting them to debug undocumented legacy systems creates a hostile environment. Operating unsafe systems burns people out.

## Operational Practices

Operational safety requires continuously evaluating risk and designing mitigations.

* **Prioritize Safe Failure Modes:** When reviewing a design, the most important question isn't "How does this work?" but "How does this fail?" If the failure mode is catastrophic, reject the design.
* **Invest in Paved Roads:** Provide standardized, automated tooling (CI/CD, observability, infrastructure as code) so the right way is the easiest way. If developers have to invent their own deployment scripts, they will invent their own outages.

Safety isn't the absence of failure. It's the presence of resilience.
