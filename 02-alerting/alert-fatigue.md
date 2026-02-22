# Alerting: Alert Fatigue

## The Reality of Production Signals

In any environment where humans must respond to automated signals, alert fatigue isn't a possibility; it's an inevitability if left unmanaged. It's the psychological and physical exhaustion that happens when engineers are bombarded with high-volume, low-value notifications. In production operations, human attention is a finite, easily depleted resource.

## Where We Go Wrong

Most teams treat monitoring as a technical problem rather than a human one. They define "good monitoring" as having an alert for every possible failure mode. When an incident occurs that wasn't caught by an alert, the immediate action item is always "add another alert."

Over time, the system accumulates hundreds of alerts. Many are "warnings" (e.g., "CPU at 75%"). Some are known transient issues (e.g., "Network blip on worker node 4"). The on-call engineer's phone buzzes constantly.

## The Cost of Alert Fatigue

The consequences of alert fatigue aren't just annoying; they actively threaten system reliability and team health.

* **Normalization of Deviance:** When an engineer receives 10 pages a week for "Database High CPU" that always resolve themselves within 5 minutes, they learn to ignore that alert. When the CPU spikes because of a catastrophic query plan that will take down the site, they'll still ignore it. This is how major outages happen.
* **Burnout and Attrition:** Being on-call in a noisy environment is psychological torture. Engineers dread their rotation. They sleep poorly, they can't focus on feature work, and eventually, they quit. High turnover in SRE and platform teams is almost always linked to alert fatigue.
* **The "Boy Who Cried Wolf" Outage:** When a critical alert is buried in a sea of trivial warnings, response time degrades. The engineer has to sift through the noise to find the actual signal, extending the Mean Time To Resolution (MTTR).

## An Operationally Sound Approach

Combating alert fatigue requires a ruthless, ongoing process of pruning and tuning. It is an engineering management responsibility, not just an individual contributor's task.

1. **The "No Action, No Alert" Rule:** This is the golden rule. If an alert fires and the correct response is "Let's wait 5 minutes and see if it recovers," that alert is broken. Delete it, or increase the evaluation window (e.g., "CPU > 90% for 10 minutes").
2. **Separate Pages from Tickets:**
    * **Pages (Wake up/Interrupt):** Reserved exclusively for immediate, actionable customer impact (e.g., "Checkout error rate > 5%").
    * **Tickets (Handle during business hours):** Used for impending issues that require attention but not immediate interruption (e.g., "Database disk will be full in 4 days," or "SSL certificate expires in 14 days").
3. **The Weekly Review:** Every on-call handoff must include a review of the noisiest alerts from the past week. The outgoing engineer must identify the top 3 offenders and create tickets to either fix the underlying issue or tune the alert threshold.

## Decision-Making Under Pressure

The critical decision in managing alert fatigue is prioritizing silence over theoretical coverage.

* **Delete the "Just in Case" Alerts:** It's terrifying to delete an alert that has been running for a year, even if it has never been useful. The fear is always, "What if it fires tomorrow and it's real?" The operational reality is that the noise is a guaranteed, daily tax on your team's sanity. The theoretical edge-case outage is a distant risk. Optimize for sanity.
* **Acknowledge and Act:** When an alert fires, acknowledge it immediately. If you realize it's noise, don't just close it. File a ticket immediately to tune or delete the alert. Do not let the noise fester.

A quiet pager isn't a sign of a broken monitoring system; it's the hallmark of a mature, well-engineered operational culture.
