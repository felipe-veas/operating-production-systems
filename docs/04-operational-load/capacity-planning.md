# Operational Load: Capacity Planning

## The Delusion of Infinite Cloud Elasticity

Cloud computing sold engineering organizations a dangerous myth: capacity planning is obsolete because infrastructure infinitely and instantly auto-scales.

This is operationally false. Cloud providers have near-infinite hardware, but your architecture does not scale infinitely. Spinning up 100 new frontend pods will not gracefully absorb a 10x traffic spike if your central PostgreSQL database maxes out its connection pool, or if a legacy third-party API rate-limits your requests.

## Where We Go Wrong

Organizations often treat capacity planning as a reactive exercise, scrambling the week before Black Friday or immediately after an overload outage.

Teams fail when they equate "auto-scaling is enabled" with "we are resilient to traffic spikes." They ignore the physics of scaling: the speed of a traffic spike versus the time it takes an orchestrator to provision a node, pull a 2GB image, start a JVM, warm the cache, and register with the load balancer. By the time new capacity is ready, the system has already crashed.

## The Cost of Reactive Capacity

Hitting hard capacity limits without a plan results in catastrophic, cascading failures.

* **The Thundering Herd:** The database slows down under load. Incoming requests pile up in the API gateway waiting for connections. The gateway runs out of memory and OOM-kills. When the orchestrator restarts the gateway, thousands of queued clients instantly retry, immediately crushing the database again. The system enters a death spiral.
* **Financial Ruin by Auto-Scaling:** A poorly configured auto-scaler reacts to a memory leak by constantly spinning up massive instances. The resulting cloud bill wipes out the quarter's margins.
* **The "Busy Waiting" Outage:** During a spike, engineers spend hours manually tuning resource limits and pleading with vendor support for quota increases. They are paralyzed from actually fixing the software bottleneck.

## An Operationally Sound Approach

Mature capacity planning is a continuous, automated engineering discipline. It assumes hard limits exist and defines exactly how the system behaves when it hits them.

1. **Find the Breaking Point (Load Testing):** You cannot plan capacity if you don't know where the system breaks. Run automated, synthetic load tests simulating 2x, 5x, and 10x peak traffic. The goal isn't to see *if* it breaks, but to document exactly *what component* breaks first (the bottleneck).
2. **Graceful Degradation (Load Shedding):** When the system hits its absolute limit, it must not crash. It must aggressively shed load. Returning a fast `503 Service Unavailable` to 20% of users is better than allowing a queue to back up and timing out 100% of users. Protect the core business flow by disabling non-critical features (e.g., turning off recommendations to keep checkout alive).
3. **Know Your Quotas:** Every cloud provider imposes hard limits (e.g., IPs per VPC, API calls per second, concurrent serverless functions). Monitor your consumption of these quotas and alert at 80% capacity. Hitting a silent cloud quota during an outage is an unforced error.

## Decision-Making

The critical decision in capacity planning is admitting you cannot serve everyone all the time.

* **Implement Circuit Breakers:** If a downstream service struggles under load, the upstream service must stop sending it traffic (open the circuit). Give the struggling service time to recover. If you don't, you will kill it.
* **Over-Provisioning vs. Auto-Scaling:** For critical systems with unpredictable, spiky traffic, auto-scaling is too slow. Accept the financial cost of over-provisioning baseline capacity to absorb the initial shock while the auto-scaler catches up.

Capacity isn't just paying for more servers; it's engineering your software to survive when the servers run out.
