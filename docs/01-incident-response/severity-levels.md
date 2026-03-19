# Incident Response: Severity Levels

## Measuring Impact

When an alert fires, the immediate question is: *How bad is this?* Production impact is rarely binary. A timeout on an internal admin tool is fundamentally different from the primary checkout flow throwing 500s. The operational challenge is quantifying this impact consistently while under pressure.

## The Subjectivity Trap

Many organizations rely on subjective, emotionally driven severity levels. If an executive spots a CSS glitch, it gets escalated to a SEV1. Meanwhile, a silent failure in a background worker dropping refund events goes unnoticed because no one is complaining. A severity matrix fails when it is based on technical symptoms ("The database is down") rather than business impact ("Users cannot complete purchases").

## Operational Cost of Misalignment

Misclassifying incidents degrades your engineering culture:

* **Alert Fatigue:** If every issue is treated as a critical emergency, responders stop trusting the pager. Waking an engineer at 3:00 AM for a SEV1 that turns out to be a delayed log pipeline destroys morale.
* **Resource Burn:** Spinning up an all-hands response for a minor degradation pulls engineers off product work and kills velocity.
* **SLA Breaches:** Under-classifying a severe incident means you don't page the right SMEs fast enough, burning error budgets and violating SLAs.

## Objective Severity Definitions

Severity levels must be deterministic and strictly tied to customer impact. The definitions should eliminate debate.

* **SEV1 (Critical):** A core business flow is broken for a significant percentage of users. No workaround exists. Revenue or reputation is actively burning (e.g., "Checkout is failing for >10% of traffic"). Requires an immediate, 24/7 all-hands response.
* **SEV2 (High):** A core feature is degraded, but a workaround exists, or the blast radius is limited to a small subset of users (e.g., "Password resets are delayed by 30 minutes"). Requires an immediate response during business hours; pages the primary on-call off-hours.
* **SEV3 (Medium):** A minor feature is broken or internal tooling is degraded. No immediate customer impact (e.g., "Internal BI dashboard data is stale"). Handled during normal business hours via the ticketing queue.
* **SEV4 (Low):** Minor bugs, typos, or cosmetic issues. Triaged to the backlog.

## Assigning Severity Under Pressure

You must assign a severity level within the first five minutes of an incident. It should not be a negotiation. If the impact is ambiguous, the operational standard is to *declare a higher severity initially, and downgrade once the blast radius is understood*.

Never base severity on the technical complexity of the fix. A missing environment variable that takes down the API is a SEV1. A catastrophic database corruption on a deprecated, unused microservice is a SEV3. Severity measures customer pain, not engineering effort.
