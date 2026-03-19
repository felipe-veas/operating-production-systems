# Alerting: Alert Fatigue

## Production Realities

Alert fatigue is inevitable if unmanaged. It happens when engineers are bombarded with high-volume, low-value notifications. In production, human attention is a finite resource. If you exhaust it on noise, you won't have it when a real incident hits.

## Common Anti-Patterns

Many teams treat monitoring as a technical problem rather than a human one. They define "good monitoring" as having an alert for every possible failure mode. When an incident slips past the monitors, the default action item is always "add another alert."

Over time, the system accumulates hundreds of alerts. Most are warnings like "CPU at 75%" or known transient issues like "Network blip on worker node 4." The on-call engineer's phone buzzes constantly, training them to ignore the pager.

## Operational Impact

Alert fatigue actively threatens system reliability and team health:

* **Normalization of Deviance:** If an engineer gets paged 10 times a week for a self-resolving "Database High CPU", they learn to ignore it. When a catastrophic query plan actually threatens the site, they'll ignore that too. This is how major outages happen.
* **Burnout and Attrition:** Noisy on-call rotations destroy teams. Engineers sleep poorly, dread their shifts, and eventually quit. High turnover in platform and SRE teams is almost always linked to pager noise.
* **Inflated MTTR:** When a critical alert is buried in a sea of trivial warnings, response time degrades. The engineer has to sift through the noise to find the actual signal.

## Operational Standards

Combating alert fatigue requires ruthless, ongoing pruning. It's an engineering management responsibility, not just a chore for individual contributors.

1. **The "No Action, No Alert" Rule:** If an alert fires and the correct response is "let's wait 5 minutes and see if it recovers," the alert is broken. Delete it, or increase the evaluation window (e.g., `CPU > 90% for 10m`).
2. **Separate Pages from Tickets:**
    * **Pages (Interrupt):** Reserved exclusively for immediate, actionable customer impact (e.g., `Checkout error rate > 5%`).
    * **Tickets (Business hours):** Used for impending issues that require attention but not immediate interruption (e.g., `Database disk full in 4 days`, `SSL certificate expires in 14 days`).
3. **The Weekly Review:** Make alert tuning part of the on-call handoff. The outgoing engineer must identify the top 3 noisiest alerts and create tickets to fix the underlying issue or tune the threshold.

## Prioritizing Signal

The critical decision in managing alert fatigue is prioritizing silence over theoretical coverage.

* **Delete "Just in Case" Alerts:** It feels risky to delete an alert that has been running for a year, even if it's never been useful. But noise is a guaranteed daily tax on your team's sanity. The theoretical edge-case outage is a distant risk. Optimize for a quiet pager.
* **Acknowledge and Act:** When a noisy alert fires, don't just close it. File a ticket immediately to tune or delete it. Don't let the noise fester.

A quiet pager isn't a sign of a broken monitoring system; it's the hallmark of a mature operational culture.
