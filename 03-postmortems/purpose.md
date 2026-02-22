# Postmortems: Purpose

## The Return on Investment

Every production incident is an unplanned, expensive investment in your system's reliability. You've already paid the cost in downtime, engineer fatigue, and lost customer trust. The postmortem is the only mechanism you have to ensure a return on that investment. Without it, the same failures will repeat, and the system will remain brittle.

## Where We Go Wrong

Most organizations treat postmortems as a bureaucratic chore—a document to fill out so management can check a box and declare the incident "closed." They are often rushed, written by a single engineer who just wants to get back to feature work, and filed away in a wiki no one reads. The document focuses exclusively on the immediate technical trigger ("The Redis node ran out of memory") rather than the systemic vulnerabilities that allowed the trigger to cause an outage.

## The Cost of Bureaucratic Postmortems

When postmortems are treated as paperwork, the consequences are predictable and severe:

* **Recurring Outages:** The same class of errors will happen again because the underlying systemic issues (e.g., lack of rate limiting, insufficient testing, poor architectural boundaries) were never addressed.
* **Wasted Effort:** Engineers spend hours writing documents that result in zero operational improvements.
* **Culture of Apathy:** When engineers see that postmortems don't lead to change, they stop putting effort into them. The incident response process becomes a cynical exercise.

## An Operationally Sound Approach

The sole purpose of a postmortem is **organizational learning and systemic improvement**. It isn't a timeline of what happened; it's a deep analysis of *why* it happened and *how* to prevent it (or drastically reduce its impact) in the future.

1. **Trigger vs. Root Cause:** A mature postmortem distinguishes between the trigger (the bad code push) and the root causes (the CI/CD pipeline didn't catch it, the deployment wasn't canary-released, the service lacked bulkheads to contain the failure).
2. **Focus on the System, Not the Human:** Systems should be designed to absorb human error. If a single typo can take down production, the problem isn't the typo; the problem is the fragile system that allowed the typo to reach production unvalidated.
3. **The "Five Whys":** Relentlessly ask "Why?" until you hit a systemic, procedural, or architectural flaw. "Why did the database crash? High CPU. Why high CPU? A bad query. Why a bad query? A missing index. Why a missing index? The schema migration wasn't reviewed by a DBA."

## Decision-Making

The critical decision regarding postmortems isn't *how* to write them, but *when* to require them.

* **Criteria for a Postmortem:** You don't need a postmortem for every minor alert. Establish clear thresholds. Every SEV1 and SEV2 incident must have a postmortem. Any incident involving data loss, security breaches, or significant SLA violations requires one.
* **The Postmortem Review Meeting:** Writing the document is only half the process. The postmortem must be reviewed in a synchronous meeting with engineering leadership and relevant stakeholders. This meeting is where the organization officially commits to funding the action items required to fix the systemic flaws.

A postmortem is a contract: the team investigates the failure deeply, and management commits to prioritizing the resulting work. If either side fails, the process is useless.
