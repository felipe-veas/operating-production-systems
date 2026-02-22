# Postmortems: Investigation

## The Reality of Production Failures

When a major incident is finally mitigated and the system is stable, the immediate impulse is to close the ticket and get back to the sprint board. The outage is over; the bleeding has stopped. However, the immediate trigger—the thing you fixed to restore service—is rarely the most interesting or dangerous part of the failure. The real threats are the systemic vulnerabilities that allowed the trigger to escalate into an outage.

## Where We Go Wrong

Most postmortem investigations are shallow. They stop at the immediate technical cause: "The database ran out of connections because of a traffic spike." The action item is to bump the connection pool limit, and the postmortem is closed. This is operational malpractice. It guarantees that the next traffic spike will simply find the next bottleneck.

Teams fail because they treat the investigation as a documentation exercise rather than a forensic engineering process.

## The Cost of Shallow Investigations

When investigations lack depth, the organization pays a compounding tax on reliability.

* **Treating Symptoms, Not Diseases:** You fix the connection pool, but you never ask *why* the traffic spiked (was it a retry storm from a failing downstream service?) or *why* the application didn't gracefully degrade when the database slowed down.
* **Recurring Outages:** Because the systemic flaws remain, the same class of failure will happen again, perhaps triggered by a different component. You're constantly fighting fires instead of fireproofing the building.
* **Wasted Effort:** An investigation that concludes "the engineer typed the wrong command" and results in an action item to "be more careful" is a complete waste of organizational time.

## An Operationally Sound Approach

A rigorous investigation requires relentless curiosity and a structured methodology for digging beneath the surface. This is the core engineering work of reliability.

1. **The Timeline is the Foundation:** A highly detailed, minute-by-minute timeline of the incident is non-negotiable. It must include when the issue started, when alerts fired (or didn't), when humans engaged, what actions they took, and when mitigation occurred. This timeline is the factual basis for all subsequent analysis.
2. **The "Five Whys" Technique:** Do not accept the first answer. Force the investigation deeper.
    * *Problem:* The API went down.
    * *Why?* The pods were OOMKilled.
    * *Why?* A new deployment introduced a memory leak.
    * *Why?* The leak only happens under heavy load, which wasn't tested in staging.
    * *Why?* We don't have load testing in our CI/CD pipeline.
    * *Why?* It was deprioritized last quarter to ship features faster.
    * *Root Cause:* A deliberate business decision to accept risk in the deployment pipeline.
3. **Investigate the Response:** The investigation must analyze how the team handled the incident. Did the right alerts fire? Was the escalation path clear? Did the incident commander function effectively? How long did mitigation take, and why?

## Decision-Making

The critical decision in any investigation is determining when to stop digging.

* **Stop When You Hit a Systemic, Actionable Flaw:** You have found the root cause when you identify a procedural, architectural, or tooling deficiency that, if fixed, would prevent this class of failure entirely.
* **Investigate Near-Misses:** Mature organizations don't wait for a SEV1 outage to conduct a deep investigation. They investigate "near-misses"—incidents that *almost* took down production but were caught by a lucky coincidence or a heroic manual intervention. These are free lessons in system fragility.

An investigation is an autopsy of a failure. If you don't find a systemic cause, you haven't looked hard enough.
