# Ownership: Handoffs

## The Vulnerability of Transition

Production environments shift constantly due to re-orgs, architectural changes, and deprecations. The most vulnerable moment in a service's lifecycle is the handoff: when operational responsibility transfers between teams, or when a key engineer leaves with undocumented context.

## Where We Go Wrong

Organizations often treat handoffs as administrative trivia—a Slack message asking to update the PagerDuty schedule. They assume Git access equals ownership.

This is a massive operational risk. Having access to the code does not mean understanding the system's failure modes, deployment quirks, or operational boundaries.

## The Cost of Poor Handoffs

Without a rigorous handoff, the receiving team inherits a black box they are afraid to touch.

* **The Orphaned Outage:** Months after the transfer, the service fails at 2:00 AM. The new on-call engineer doesn't know how to debug the legacy code, where the logs live, or how to safely restart the process. MTTR spikes.
* **Fear-Driven Stagnation:** The new owners avoid refactoring, upgrading dependencies, or deploying changes because they lack the context to do so safely. The system rots into a security and reliability liability.
* **Resentment and Blame:** When the service breaks, the new team blames the old team for bad code, and the old team blames the new team for breaking it.

## An Operationally Sound Approach

Treat service handoffs as a formal process requiring explicit proof of operational readiness. It is a negotiation, not a mandate.

1. **The Readiness Checklist:** Complete a documented checklist before transferring the pager. The receiving team must have:
    * Verified access to repositories, CI/CD pipelines, and Infrastructure as Code.
    * Working access to dashboards, logs, and alerts.
    * An understanding of the architecture, dependencies, and known failure modes.
    * Tested runbooks for routine operations (deploy, rollback, restart, scale).
2. **The Shadow Period:** The receiving team shadows the outgoing team's on-call rotation for at least two weeks. They actively participate in incidents and deployments to absorb undocumented tribal knowledge.
3. **The Reverse Shadow Period:** For the following two weeks, the receiving team takes primary on-call, but the outgoing team acts as their dedicated escalation path. The new team holds the pager with a safety net.

## Decision-Making

The most critical part of a handoff is the authority to say "No."

* **The Right of Refusal:** The receiving team must have the authority to reject a handoff if the service fails readiness criteria (e.g., outdated runbooks, abysmal test coverage, manual deployment steps).
* **No Ownership Without Investment:** If a handoff is rejected, the business must either allocate time for the outgoing team to pay down the operational debt, or accept the risk of decommissioning the service. You cannot force a team to operate software they don't trust.

A successful handoff transfers context and operational confidence, not just a Git repository.
