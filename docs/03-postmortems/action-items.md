# Postmortems: Action Items

## The Reality of Action Items

A postmortem document doesn't improve reliability. No matter how insightful the investigation or blameless the culture, the only thing that changes the physical reality of your production systems is the resulting engineering work. Action items are the currency of reliability.

## The Trap of Vague Actions

Most postmortems fail at the very end. Teams conduct thorough investigations, identify root causes, and then write vague, untrackable action items that are ultimately ignored.

"Improve monitoring," "investigate better rate limiting," "add more tests," or "be more careful when deploying" are not action items. They are aspirations. They go into a backlog and die there. When action items are weak or ignored, incident response becomes performative. The team feels like they solved the problem by writing a document, but the system remains exactly as fragile as it was before the outage. The same failure mode will happen again, and engineers will stop putting effort into investigations because they know the work won't be prioritized.

## Writing Effective Action Items

Treat action items with the same rigor as product features. They must be specific, measurable, assigned, and ruthlessly prioritized.

1. **Make them concrete:** "Add a Datadog monitor for when the `users` DB connection pool exceeds 80% for 5 minutes" instead of "Improve DB monitoring." The PR is either merged or it isn't.
2. **Assign a single owner:** Every action item needs one human owner. Not a team, not a Slack channel. A specific person.
3. **Track them:** Every action item must be a ticket in your issue tracker, linked directly to the postmortem, with a deadline—usually within the next sprint.

Categorize the work to clarify its impact:

* **Prevent (P0):** Engineering work that physically prevents this class of failure from happening again (e.g., "Implement circuit breakers in the downstream service call").
* **Detect (P1):** Work that ensures we know immediately if it happens again (e.g., "Add SLO alert for checkout latency").
* **Mitigate (P2):** Work that reduces impact or speeds up recovery (e.g., "Write a runbook for safely draining the Redis cache").

## Prioritization and Execution

The critical decision regarding action items is prioritization. The postmortem review meeting is where this happens. If an action item is critical to preventing a SEV1 outage, it must displace planned feature work in the next sprint. If management refuses to prioritize it, the business is explicitly accepting the risk of recurrence.

Apply the "Rule of Three." Do not create 20 action items from a single incident. You will never finish them, and they will just clutter the backlog. Identify the top three highest-leverage fixes—ideally one Prevent, one Detect, and one Mitigate—and execute them.

An action item that isn't scheduled in a sprint is just a wish. Reliability requires engineering capacity, not just good intentions.
