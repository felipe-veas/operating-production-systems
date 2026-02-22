# Ownership: Developers and Operations

## The Wall of Confusion

The historical relationship between software development and IT operations is fundamentally broken. It's a tale of two distinct cultures, two different toolchains, and opposing incentives. Developers are paid to write code and ship features—to change the system as fast as possible. Operations (SysAdmins, DBAs, early SREs) are paid to keep the system stable and available, which inherently means resisting change. When these forces collide, the result is friction, bureaucracy, and fragile software.

## Where We Go Wrong

The failure mode in this dynamic is the "Wall of Confusion." Developers write code on their laptops, push it to a repository, and consider their job done. They throw the compiled artifact over the wall to Operations.

Operations, who have no context on how the code works, its failure modes, or its performance characteristics, are suddenly responsible for deploying it, configuring the network, managing the database schema, and waking up at 3:00 AM when the application inevitably crashes.

This model fails because it completely separates the act of creating complexity from the pain of managing it.

## The Cost of the Wall

When developers and operations are siloed, the consequences are disastrous for both velocity and reliability.

* **The "Works on My Machine" Outage:** Developers test code against a local SQLite database with 10 rows. Operations deploys it against a clustered PostgreSQL database with 10 million rows. The application deadlocks. The developer blames the database; the DBA blames the code.
* **The Deployment Bottleneck:** Because Operations doesn't trust the code, they institute massive Change Advisory Boards (CABs). Deployments take weeks of approvals, manual testing, and high-risk release nights.
* **Misaligned Incentives:** Developers have no incentive to write operationally sound code (logging, metrics, graceful degradation) because they don't have to debug it in production. They never feel the pain of a bad architectural decision.

## An Operationally Sound Approach

The only sustainable model for operating complex systems is to tear down the wall and merge development and operations into a single, continuous lifecycle. This is the core principle of DevOps and modern Site Reliability Engineering (SRE).

1. **You Build It, You Run It:** The team that writes the code is responsible for its design, deployment, performance, and on-call rotation. There is no separate "Ops" team to hand off to.
2. **Operations as a Discipline, Not a Department:** Operations is no longer a job title; it's a set of engineering skills (Infrastructure as Code, CI/CD, observability, incident response) that every developer must possess to some degree.
3. **SRE as Enabler, Not Gatekeeper:** The role of the SRE (or Platform Engineer) shifts from "deploying code and fighting fires" to building the self-service tools, platforms, and automation that empower developers to own their code in production safely.

## Decision-Making

The critical decision in bridging this gap is how the organization handles failure.

* **The Blameless Postmortem of the Deploy:** When a bad deployment causes an outage, the postmortem must not ask "Why did Operations let this through?" or "Why did the developer write bad code?" It must ask, "Why did our automated CI/CD pipeline fail to catch the error in staging? Why didn't we canary the release? Why did the failure cascade?"
* **The Authority to Halt the Line:** If a development team's service is consistently failing and burning out their on-call rotation, the SRE team (or engineering leadership) must have explicit authority to halt new feature development on that service until the reliability issues are fixed.

The goal isn't to force developers to become sysadmins, but to create a culture where the pain of operating a system is felt directly by the people designing it. When developers hold the pager for their own code, the code magically becomes more robust, easier to monitor, and safer to deploy.
