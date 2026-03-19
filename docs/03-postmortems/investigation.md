# Postmortems: Investigation

## Beyond the Immediate Fix

When a major incident is mitigated and the system stabilizes, the immediate impulse is to close the ticket and get back to the sprint board. The bleeding has stopped. However, the immediate trigger—the thing you fixed to restore service—is rarely the most dangerous part of the failure. The real threats are the systemic vulnerabilities that allowed the trigger to escalate into an outage.

## The Danger of Shallow Investigations

Most postmortem investigations stop at the immediate technical cause: "The database ran out of connections because of a traffic spike." The team bumps the connection pool limit and closes the document. This guarantees that the next traffic spike will simply find the next bottleneck.

Treating the investigation as a documentation exercise rather than a forensic engineering process results in a compounding tax on reliability. You treat symptoms, not diseases. You fix the connection pool, but you never ask *why* the traffic spiked (was it a retry storm from a failing downstream service?) or *why* the application didn't gracefully degrade. Because the systemic flaws remain, the same class of failure will happen again.

## Forensic Engineering

A rigorous investigation requires a structured methodology for digging beneath the surface. This is the core engineering work of reliability.

1. **Build a factual timeline:** A highly detailed, minute-by-minute timeline of the incident is non-negotiable. It must include when the issue started, when alerts fired (or didn't), when humans engaged, what actions they took, and when mitigation occurred. This timeline is the factual basis for all subsequent analysis.
2. **Use the "Five Whys":** Do not accept the first answer. Force the investigation deeper.
    * *Problem:* The API went down.
    * *Why?* The pods were OOMKilled.
    * *Why?* A new deployment introduced a memory leak.
    * *Why?* The leak only happens under heavy load, which wasn't tested in staging.
    * *Why?* We don't have load testing in our CI/CD pipeline.
    * *Why?* It was deprioritized last quarter to ship features faster.
    * *Root Cause:* A deliberate business decision to accept risk in the deployment pipeline.
3. **Investigate the response:** Analyze how the team handled the incident. Did the right alerts fire? Was the escalation path clear? How long did mitigation take, and why?

## Knowing When to Stop

The critical decision in any investigation is determining when to stop digging. You have found the root cause when you identify a procedural, architectural, or tooling deficiency that, if fixed, would prevent this class of failure entirely.

Mature organizations don't wait for a SEV1 outage to conduct a deep investigation. They investigate "near-misses"—incidents that almost took down production but were caught by a lucky coincidence or heroic manual intervention. These are free lessons in system fragility.

An investigation is an autopsy of a failure. If you don't find a systemic cause, you haven't looked hard enough.
