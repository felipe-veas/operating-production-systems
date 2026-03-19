# Ownership: Developers and Operations

## The Wall of Confusion

The traditional split between software development and IT operations creates conflicting incentives. Developers are rewarded for shipping features and changing the system quickly. Operations (SysAdmins, DBAs, traditional SREs) are rewarded for stability, which usually means resisting change. This structural friction leads to bureaucracy and fragile deployments.

## Where We Go Wrong

The classic failure mode is the "Wall of Confusion." Developers write code locally, merge it, and consider their job done. They throw the artifact over the wall to Operations.

Operations inherits a black box. Without context on the application's failure modes or performance characteristics, they are suddenly responsible for deploying it, provisioning infrastructure, and waking up at 3:00 AM when it crashes.

This model fails because it separates the people creating complexity from the people feeling the pain of managing it.

## The Cost of the Wall

Siloing development and operations destroys both velocity and reliability.

* **The "Works on My Machine" Outage:** A developer tests against a local SQLite database with ten rows. Operations deploys against a clustered PostgreSQL database with ten million rows. The application deadlocks. The developer blames the database; the DBA blames the code.
* **The Deployment Bottleneck:** Because Operations lacks confidence in the code, they mandate Change Advisory Boards (CABs). Deployments degrade into weeks of approvals, manual testing, and high-risk, late-night releases.
* **Misaligned Incentives:** Developers have no reason to prioritize operational features like structured logging, metrics, or graceful degradation if they never debug production incidents. They don't feel the consequences of bad architectural decisions.

## An Operationally Sound Approach

Operating complex systems requires merging development and operations into a single lifecycle.

1. **You Build It, You Run It:** The team writing the code owns its deployment, performance, and on-call rotation. There is no separate "Ops" team to catch the pager.
2. **Operations as a Discipline, Not a Department:** Operations stops being a job title. It becomes a set of engineering skills—Infrastructure as Code, CI/CD, observability, incident response—that every developer needs.
3. **SRE as Enabler, Not Gatekeeper:** SREs and Platform Engineers stop deploying code and fighting fires for other teams. Instead, they build self-service tooling and paved roads that let developers safely own their code in production.

## Decision-Making

Bridging this gap requires changing how the organization handles failure.

* **Systemic Postmortems:** When a deployment causes an outage, stop asking "Why did Operations let this through?" or "Why did the developer write bad code?" Ask systemic questions: "Why did the CI/CD pipeline miss this in staging? Why didn't the canary catch it? Why did the failure cascade?"
* **Authority to Halt the Line:** If a service consistently fails and burns through its error budget, engineering leadership must halt feature development. The team focuses entirely on reliability until the service stabilizes.

The goal isn't turning developers into sysadmins. It's ensuring the pain of operating a system is felt by the people designing it. When developers hold the pager for their own code, that code quickly becomes more robust, observable, and safer to deploy.
