# Ownership: Service Ownership

## The Ambiguity of Microservices

In a microservices or distributed architecture, the lines between who built a system, who runs it, and who fixes it when it breaks are often dangerously blurred. When an alert fires for the `user-profile` service at 2:00 AM, the most critical question isn't "What is broken?" but "Whose pager is ringing?" If the answer is an SRE who has never seen the codebase, or worse, no one at all, the system's reliability is fundamentally compromised.

## Where We Go Wrong

The classic anti-pattern in software engineering is the "throw it over the wall" model. Developers write the code, merge the PR, and declare the feature "done." Operations or SRE teams are then expected to deploy it, monitor it, and wake up when it fails.

This model fails because it completely misaligns incentives. Developers are incentivized to ship features as fast as possible, regardless of operational fragility, because they don't feel the pain of operating those features. SREs are incentivized to block deployments and add bureaucratic gates because they are terrified of being paged for code they didn't write and don't understand.

## The Cost of Ambiguous Ownership

When service ownership is ambiguous or divorced from the development lifecycle, the consequences are severe:

* **Orphaned Services:** Services run in production that no active team claims. When they inevitably break or require a security patch, it causes a cross-team crisis to figure out who has the context (and permission) to fix them.
* **High MTTR:** An SRE debugging a memory leak in a Java application they didn't write will take exponentially longer than the developer who wrote the garbage collection logic.
* **Toxic Culture:** The relationship between Development and Operations becomes adversarial. SREs become the "Department of No," and developers view operations as an impediment to velocity.

## An Operationally Sound Approach

The only sustainable model for operating complex software is full lifecycle service ownership: **You build it, you run it.**

1. **Code to Grave:** The team that writes the code is responsible for its design, deployment, performance, monitoring, and on-call rotation.
2. **The Ownership Registry:** There must be a central, programmatic registry (e.g., Backstage, OpsLevel, or a simple YAML file in a central repo) mapping every running service to a specific, active engineering team. "Unknown" is not a valid owner.
3. **The Role of SRE:** In this model, SREs do not carry the pager for product services. Instead, SREs build the "paved road"—the tooling, platforms, and automation (CI/CD, observability, Infrastructure as Code) that make it easy and safe for developers to own their services in production.

## Decision-Making

The critical decision in enforcing service ownership is how leadership handles "orphaned" code.

* **No Code Without an Owner:** If a team is disbanded or re-orged, their services cannot be left running without a new owner explicitly accepting the pager for them. If no team is willing to own a service, the business must make the hard decision to decommission it. You can't run software in production based on hope.
* **The Pager Handoff Readiness Review:** Before a new service is allowed into production, the owning team must demonstrate operational readiness: runbooks are written, alerts are tuned, dashboards exist, and the team is trained on the deployment pipeline. Ownership is a privilege earned through rigor, not a right granted by merging code.

Service ownership isn't about punishing developers with pagers; it's about creating the tight feedback loop required to build resilient software. You can't build a reliable system if the people building it never experience its failures.
