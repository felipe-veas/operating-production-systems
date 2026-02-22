# Postmortems: Action Items

## The Reality of Production Failures

A postmortem document, no matter how insightful the investigation or how blameless the culture, does not improve reliability. The only thing that changes the physical reality of your production systems is the action items—the actual engineering work that results from the investigation.

## Where We Go Wrong

Most postmortems fail at the very end. The investigation is thorough, root causes are identified, and then the team writes a list of action items that are vague, untrackable, and ultimately ignored.

"Improve monitoring." "Investigate better rate limiting." "Add more tests." "Be more careful when deploying." These aren't action items; they are aspirations. They go into a Jira backlog and die there.

## The Cost of Aspirational Action Items

When action items are weak or ignored, the entire incident response process becomes performative.

* **The Illusion of Progress:** The team feels like they've solved the problem because they wrote a document, but the system is exactly as fragile as it was the day before the outage.
* **Recurring Outages:** The same failure mode will happen again, often within weeks, because the systemic vulnerabilities were never actually fixed.
* **Engineering Cynicism:** When engineers see that postmortem action items are never prioritized by product management, they stop putting effort into investigations. The process becomes a bureaucratic tax.

## An Operationally Sound Approach

Action items are the currency of reliability. Treat them with the same rigor as product features. They must be specific, measurable, assigned, and ruthlessly prioritized.

1. **The "SMART" Framework (Adapted for Reliability):**
    * *Specific:* "Add an alert for when the `users` database connection pool exceeds 80% for 5 minutes." (Not "Improve DB monitoring").
    * *Measurable:* The PR is merged, or it isn't. The alert is firing in Datadog, or it isn't.
    * *Assigned:* Every action item needs a single human owner. Not a team, not a vague entity. A person.
    * *Trackable:* Every action item must be a ticket in your issue tracker and linked directly to the postmortem.
    * *Time-Bound:* Every action item needs a deadline, usually within the next sprint.
2. **Categories of Mitigation:**
    * **Prevent (P0):** Engineering work that physically prevents this class of failure from happening again (e.g., "Implement circuit breakers in the downstream service call").
    * **Detect (P1):** Work that ensures we know immediately if it happens again (e.g., "Add SLO alert for checkout latency").
    * **Mitigate (P2):** Work that reduces impact or speeds up recovery (e.g., "Write a runbook for safely draining the Redis cache").

## Decision-Making

The critical decision regarding action items is prioritization, and it is a management decision.

* **Fund the Reliability Work:** The postmortem review meeting is the mechanism for prioritizing action items. If an action item is critical to preventing a SEV1 outage, it must displace planned feature work in the next sprint. If management refuses to prioritize it, the business is explicitly accepting the risk of recurrence.
* **The "Rule of Three":** Do not create 20 action items from a single incident. You will never finish them, and they'll just clutter the backlog. Identify the top 3 highest-leverage fixes (usually one Prevent, one Detect, and one Mitigate) and execute them flawlessly.

An action item that isn't scheduled in a sprint is just a wish. Reliability requires engineering capacity, not just good intentions.
