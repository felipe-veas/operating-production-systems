# Principles: Engineering Values

## The Reality of Technical Choices

Writing the initial code is the cheapest part of software engineering. The real cost lies in maintenance, evolution, and operation. Every architectural choice, new dependency, and clever abstraction is an operational liability the team will pay for repeatedly.

## Where We Go Wrong

Engineering cultures often fail by optimizing for the short-term rush of shipping over long-term sustainability.

Teams mistake resume-driven development for engineering excellence. They adopt complex microservices for simple CRUD apps instead of picking boring, proven tools that actually fit the problem.

## Core Values

A mature engineering culture is defined by how it makes decisions under constraint.

1. **Boring Technology is Good Technology:** The best technology is the one you already know how to operate, debug, and scale. Postgres is boring. Boring technology doesn't fail in novel ways at 3:00 AM. Only adopt "exciting" tech when boring tech fundamentally fails to solve the problem.
2. **Optimize for Readability, Not Cleverness:** Code is read far more often than it's written—usually during an incident. Clever, highly abstracted code is an operational hazard. Write explicit code that clearly communicates intent.
3. **Toil is a Bug:** If a human repeatedly performs a manual task to keep a system running (e.g., restarting a leaky service, manually syncing data), it's a bug. Automate it or engineer it away.
4. **Embrace Constraints:** Infinite resources breed infinite complexity. Hard constraints (e.g., "deployments must take < 5 minutes", "maximum 3 hard dependencies") force simplicity and prevent architectural sprawl.
5. **Data Beats Opinions:** Telemetry settles arguments, not seniority. "The database feels slow" is an opinion. "P99 latency on the `users` table spiked 400ms after the deploy" is data.

## Anti-Patterns

When velocity is prioritized over sustainability, technical debt compounds until development stalls.

* **The Rewrite Trap:** Building with flavor-of-the-month frameworks without tests makes systems too fragile to modify. Teams eventually demand a rewrite, throwing away years of embedded business logic and operational hardening, only to build a second, equally flawed system.
* **Hero Culture:** Praising the engineer who works all weekend to fix a broken system—while ignoring the one who quietly refactored the pipeline to prevent the outage—incentivizes fragility. It signals that firefighting is more valuable than fire prevention.

## Operating for the Long Term

The ultimate engineering value is taking ownership of the system's long-term health.

* **Saying "No" is Engineering Work:** Saying "no" is core engineering work. "No, we don't need Kafka for this." "No, we can't ship without runbooks." Protecting the system from unnecessary complexity is high-leverage work.
* **Fund the Quiet Work:** Leadership must allocate capacity for unglamorous work: dependency upgrades, deleting dead code, and tuning alerts. Unfunded work doesn't happen.

Engineering excellence isn't about perfect code. It's about building systems we can operate safely, modify confidently, and depend on.
