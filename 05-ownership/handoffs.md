# Ownership: Handoffs

## The Vulnerability of Transition

Production environments are constantly evolving as teams re-org, architectures change, and legacy systems are deprecated. A critical vulnerability in the lifecycle of any service is the moment it changes hands—when the team that built it transfers operational responsibility to another team, or when a sole developer leaves, taking their undocumented context with them.

## Where We Go Wrong

Most organizations treat service handoffs as an administrative task—a quick Slack message saying, "Hey, we're taking over the legacy billing pipeline, can you add us to the PagerDuty schedule?" They assume that because the new team has access to the Git repository, they are now the owners.

This "throw it over the wall" approach is a massive operational risk. Teams fail because they confuse access to code with understanding the system's failure modes, operational quirks, and deployment pipelines.

## The Cost of Poor Handoffs

When a service changes hands without rigor, the new owners inherit a black box they are terrified to touch.

* **The Orphaned Outage:** Three months after the handoff, the service fails silently at 2:00 AM. The new on-call engineer has no idea how to debug the legacy Java code they inherited. They don't know where the logs are, how to restart the process safely, or who to call. MTTR skyrockets.
* **Fear-Driven Stagnation:** The new owning team refuses to refactor, upgrade dependencies, or deploy changes because they lack the context to do it safely. The system rots, becoming a security and reliability liability.
* **Resentment and Blame:** When the service inevitably breaks, the new team blames the old team for writing garbage code, while the old team blames the new team for breaking it. The culture becomes toxic.

## An Operationally Sound Approach

A mature engineering culture treats a service handoff as a formal, rigorous process requiring explicit proof of operational readiness from the receiving team. It's a negotiation, not a decree.

1. **The Readiness Checklist:** A documented checklist must be completed before the pager transfers. This ensures the receiving team has:
    * Access to all repositories, CI/CD pipelines, and Infrastructure as Code.
    * Access to monitoring dashboards, logs, and alerts.
    * Deep understanding of the architecture, dependencies, and known failure modes.
    * Clear, tested runbooks for common operational tasks (deploy, rollback, restart, scale).
2. **The Shadow Period:** The receiving team should shadow the outgoing team's on-call rotation for at least two weeks. They must actively participate in incident response, deployments, and debugging to absorb tribal knowledge that exists outside the documentation.
3. **The Reverse Shadow Period:** For the next two weeks, the receiving team is primary on-call, but the outgoing team is explicitly dedicated as their immediate escalation path. The new team holds the pager, but with a safety net while they build confidence.

## Decision-Making

The critical decision in a handoff is the authority to say "No."

* **The Right of Refusal:** The receiving team must have explicit authority to reject a handoff if the service doesn't meet readiness criteria (e.g., "The runbooks are outdated," "Test coverage is 10%," "Deployment requires manual SSH access").
* **No Ownership Without Investment:** If the receiving team rejects the handoff, the business must either allocate engineering time for the outgoing team to fix the operational debt or accept the risk of decommissioning the service. You cannot force a team to operate software they don't understand or trust.

A successful handoff isn't about transferring a Git repository; it's about transferring the context, confidence, and capability to operate the software safely in production.
