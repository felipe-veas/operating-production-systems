# Ownership: Production Culture

## The Reality of Stated Values

Every engineering organization claims to care about reliability. It shows up in company values and all-hands meetings. But an organization's true values are revealed by how it allocates its scarcest resource: engineering time. If leadership talks about reliability but only promotes engineers who ship fragile features quickly—ignoring those who quietly refactor connection pools to prevent outages—the actual culture is obvious.

## Where We Go Wrong

A broken production culture is rarely intentional. It stems from misaligned incentives and leadership failing to protect long-term system health from short-term product demands.

Teams fail when they treat production as an afterthought—a dumping ground where code goes once the "real work" of writing it is finished. This creates a systemic lack of respect for the operational environment.

## The Cost of a Feature-Factory Culture

Optimizing purely for feature delivery at the expense of operational rigor creates compounding debt. Eventually, the system collapses under its own weight.

* **The "Launch and Abandon" Anti-Pattern:** A team grinds through weekends to hit a deadline. They skip tests, hardcode configs, and ignore runbooks. The day after launch, they are reassigned. The service is orphaned in production, becoming a ticking time bomb.
* **Heroic Outage Response:** Fragile, undocumented systems cause frequent, severe outages. The organization relies on a few "heroes" with tribal knowledge to save the day. Celebrating these heroes signals that fighting fires is more valuable than preventing them.
* **Burnout and Apathy:** Engineers who care about reliability get demoralized. They watch CI/CD improvements get deprioritized for minor UI tweaks. Eventually, they leave, taking their operational discipline with them.

## An Operationally Sound Approach

A resilient production culture requires top-down enforcement of standards that prioritize long-term sustainability over short-term velocity.

1. **Reliability is a Feature:** Treat reliability as the foundational feature of any product. A feature that only works 90% of the time is a liability, not a capability.
2. **The Definition of Done:** A feature isn't "done" when the PR merges. It is done when it runs in production, emits actionable alerts, has tested runbooks, and the team is trained to support it on-call.
3. **The Error Budget as a Contract:** Service Level Objectives (SLOs) and error budgets provide an objective measure of reliability. If the error budget is exhausted, feature work stops. Engineering capacity redirects to reliability until the budget recovers. This contract between Product and Engineering must be non-negotiable.

## Decision-Making

The true test of a production culture is how leadership handles business pressure.

* **The Courage to Delay a Launch:** If a critical feature is ready, but load testing shows it will likely crash the database under peak traffic, leadership must delay the launch. Shipping a known outage is a leadership failure, not a velocity win.
* **Rewarding the Plumbers:** Actively promote engineers who do the invisible work: automating certificate rotation, migrating legacy datastores, tuning noisy alerts, and speeding up pipelines. If you only promote people who build new things, you will only get new, broken things.

A mature production culture recognizes that writing code is the easy part. Operating it safely at scale is the actual engineering challenge.
