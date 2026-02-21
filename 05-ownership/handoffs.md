# Ownership: Handoffs

## The Reality of Production Boundaries

Production environments are not static; they are constantly evolving as teams re-org, new architectures are adopted, and legacy systems are deprecated. A critical vulnerability in the lifecycle of any service is the moment it changes hands—when the team that built it transfers operational responsibility to another team, or when a developer leaves the company, taking their deep, undocumented context with them.

## Where Teams Go Wrong

Most organizations treat service handoffs as an administrative task—a quick Slack message saying, "Hey, we're taking over the legacy billing pipeline, can you add us to the PagerDuty rotation?" They assume that because the new team has access to the Git repository, they are now the owners.

This "throw it over the wall" approach is a massive operational risk. Teams fail because they confuse access to code with understanding of the system's failure modes, operational quirks, and deployment pipelines.

## The Cost of Poor Handoffs

When a service changes hands without rigor, the new owners inherit a black box that they are terrified to touch.

* **The "Orphaned" Outage:** Three months after the handoff, the service fails silently at 2:00 AM. The new on-call engineer has no idea how to debug the legacy Java code they inherited. They don't know where the logs are, how to restart the process safely, or who to call. The MTTR skyrockets.
* **Fear-Driven Stagnation:** The new owning team refuses to refactor, upgrade dependencies, or deploy changes to the inherited service because they lack the context to do it safely. The system rots, becoming a security and reliability liability.
* **Resentment and Blame:** When the service inevitably breaks, the new team blames the old team for writing "garbage code," while the old team blames the new team for "breaking it." The engineering culture becomes toxic.

## An Operationally Sound Approach

A mature engineering culture treats a service handoff as a formal, rigorous process that requires explicit proof of operational readiness from the receiving team. It is a negotiation, not a decree.

1. **The Readiness Checklist:** A formal, documented checklist must be completed before the pager is transferred. This checklist ensures the receiving team has:
    * Read access to all repositories, CI/CD pipelines, and infrastructure as code.
    * Access to all monitoring dashboards, logs, and alerts.
    * A deep understanding of the system's architecture, dependencies, and known failure modes.
    * Clear, tested runbooks for common operational tasks (deployment, rollback, restarting, scaling).
2. **The "Shadow" Period:** The receiving team should shadow the outgoing team's on-call rotation for at least two weeks. They must actively participate in incident response, deployments, and debugging sessions to absorb the tribal knowledge that inevitably exists outside the documentation.
3. **The "Reverse Shadow" Period:** For the next two weeks, the receiving team is primary on-call, but the outgoing team is explicitly dedicated as their immediate escalation path. The new team handles the pagers, but they have a safety net while they build confidence.

## Decision-Making Under Pressure

The critical decision in a handoff is the authority to say "No."

* **The Right of Refusal:** The receiving team must have the explicit authority to reject a handoff if the service does not meet the readiness criteria (e.g., "The runbooks are outdated," "The test coverage is 10%," "The deployment pipeline requires manual SSH access").
* **No Ownership Without Investment:** If the receiving team rejects the handoff, the business must either allocate engineering time for the outgoing team to fix the operational debt, or accept the risk of decommissioning the service. You cannot force a team to operate software they do not understand or trust.

A successful handoff is not about transferring a Git repository; it is about transferring the context, confidence, and capability to operate the software safely in production.
