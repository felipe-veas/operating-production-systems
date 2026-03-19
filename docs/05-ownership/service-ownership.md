# Ownership: Service Ownership

## The Ambiguity of Microservices

In distributed architectures, the lines between who builds a system, who runs it, and who fixes it are often blurred. When an alert fires for the `user-profile` service at 2:00 AM, the most critical question isn't "What broke?" but "Whose pager is ringing?" If the answer is an SRE who has never seen the codebase—or worse, no one at all—reliability is fundamentally compromised.

## Where We Go Wrong

The classic anti-pattern is the "throw it over the wall" model. Developers write code, merge the PR, and declare the feature done. Operations or SRE teams are then expected to deploy it, monitor it, and wake up when it fails.

This misaligns incentives. Developers are pushed to ship features quickly, ignoring operational fragility because they don't feel the pain of running them. SREs are pushed to block deployments and add bureaucratic gates because they are terrified of being paged for code they don't understand.

## The Cost of Ambiguous Ownership

Divorcing ownership from the development lifecycle has severe consequences:

* **Orphaned Services:** Services run in production without an active owner. When they break or need a security patch, it triggers a cross-team crisis to find someone with the context and permissions to fix them.
* **High MTTR:** An SRE debugging a memory leak in a Java app they didn't write takes exponentially longer than the developer who wrote the garbage collection logic.
* **Toxic Culture:** Development and Operations become adversarial. SRE becomes the "Department of No," and developers view operations as a roadblock to velocity.

## An Operationally Sound Approach

The only sustainable model for operating complex software is full lifecycle service ownership: **You build it, you run it.**

1. **Code to Grave:** The team writing the code owns its design, deployment, performance, monitoring, and on-call rotation.
2. **The Ownership Registry:** Maintain a central, programmatic registry (e.g., Backstage, OpsLevel, or a YAML file) mapping every running service to an active engineering team. "Unknown" is not a valid owner.
3. **The Role of SRE:** SREs do not carry the pager for product services. Instead, they build the "paved road"—the CI/CD, observability, and Infrastructure as Code tooling that makes it safe and easy for developers to own their services in production.

## Decision-Making

Enforcing service ownership comes down to how leadership handles orphaned code.

* **No Code Without an Owner:** If a team is disbanded, their services cannot keep running unless a new owner explicitly accepts the pager. If no team will own a service, the business must decommission it. You cannot run production software on hope.
* **Operational Readiness Reviews:** Before a new service enters production, the owning team must prove readiness: runbooks are written, alerts are tuned, dashboards exist, and the team understands the deployment pipeline. Ownership is a privilege earned through rigor, not a right granted by merging code.

Service ownership isn't about punishing developers with pagers. It creates the tight feedback loop necessary to build resilient software. You cannot build a reliable system if the people building it never experience its failures.
