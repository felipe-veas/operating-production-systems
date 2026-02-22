# Principles: Engineering Values

## The Reality of Technical Choices

In the lifecycle of a software product, writing the initial code is often the cheapest and easiest part. The true cost of software is measured in its maintenance, evolution, and operation over years. Every architectural decision, every new dependency, and every "clever" abstraction is a liability the organization will pay for repeatedly.

## Where We Go Wrong

The failure mode of many engineering cultures is optimizing for the short-term high of shipping code over the long-term sustainability of the system.

Teams fail when they mistake "resume-driven development" for engineering excellence. They adopt a complex, unproven microservices architecture for a simple CRUD app because it's currently popular, rather than choosing boring, reliable technology that actually fits the business problem.

## Core Values

A mature engineering culture isn't defined by its tools, but by the principles it uses to make decisions under constraint.

1. **Boring Technology is Good Technology:** The most valuable technology is the one you already know how to operate, debug, and scale. Postgres is boring. Bash is boring. Boring technology doesn't fail in novel, exciting ways at 3:00 AM. Adopt "exciting" technology only when boring technology fundamentally fails to solve a critical business problem.
2. **Optimize for Readability, Not Cleverness:** Code is read exponentially more often than it's written, usually by someone trying to figure out why production is down. Clever, overly abstracted code is an operational hazard. Write simple, explicit code that clearly communicates its intent.
3. **Toil is a Bug:** If a human has to repeatedly perform a manual task to keep the system running (e.g., restarting a leaky service, manually syncing a database), it's an engineering failure. It must be prioritized, engineered away, and automated.
4. **Embrace Constraints:** Infinite resources breed infinite complexity. Architectural constraints (e.g., "All services must deploy in under 5 minutes," "No service can have more than 3 hard dependencies") force simplicity and prevent the system from sprawling out of control.
5. **Data Beats Opinions:** In any debate about performance, reliability, or architecture, telemetry settles the argument, not the seniority of the engineer. "I think the database is slow" is an opinion. "The P99 latency of the `users` table increased by 400ms after the last deploy" is data.

## The Cost of Abandoning Core Values

When an organization abandons these values in favor of velocity at all costs, technical debt compounds until feature development grinds to a halt.

* **The Rewrite Trap:** Because the system was built using the flavor-of-the-month framework without tests or documentation, it becomes so fragile that no one dares modify it. The team demands a complete rewrite, throwing away years of embedded business logic and operational hardening, usually resulting in a second, equally flawed system.
* **The Hero Culture:** A culture that praises the engineer who works all weekend to fix a broken, undocumented system, while ignoring the engineer who spent the week quietly refactoring the deployment pipeline to prevent failures, incentivizes fragility. It tells the team that fighting fires is more valuable than preventing them.

## Decision-Making for the Long Term

The ultimate engineering value is taking ownership of the long-term health of the software.

* **Saying "No" is Engineering Work:** The most important word a Staff or Principal Engineer can say is "No." "No, we don't need Kafka for this." "No, we can't ship this without runbooks." Protecting the system from unnecessary complexity is the highest leverage work an engineer can do.
* **Fund the Quiet Work:** Engineering leadership must explicitly allocate sprint capacity for unglamorous work: upgrading dependencies, writing tests, deleting dead code, and tuning alerts. If this work isn't funded, it won't happen.

Excellence in software engineering isn't about writing perfect code; it's about building systems that humans can operate safely, modify confidently, and depend on consistently.
