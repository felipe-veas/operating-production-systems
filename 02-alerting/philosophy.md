# Alerting: Philosophy

## The Reality of Production Signals

In a sufficiently complex distributed system, something is always failing. A node is being recycled, a minor network partition is dropping packets, or a background queue is temporarily backing up. The reality of production is that raw telemetry—metrics, logs, and traces—is overwhelmingly noisy. The purpose of an alerting system is not to report every anomaly; it is to extract the actionable signal from this deafening noise and demand human attention only when the system cannot heal itself and customer pain is imminent.

## Where Teams Go Wrong

Most teams build alerting systems from the bottom up. An engineer writes a new microservice, adds a metric for CPU usage, and creates an alert if it goes over 80%. They add an alert for memory, an alert for pod restarts, and an alert for a specific database query taking longer than 100ms. They treat alerts as a debugging tool rather than an operational trigger.

## The Cost of Noise

When alerting is philosophical flawed, the consequences are immediate and toxic to the engineering culture.

* **The Boy Who Cried Wolf:** When 90% of pages do not require action (e.g., "CPU spiked for 2 minutes and recovered"), engineers learn to ignore the pager. When a real, critical failure happens, the response is delayed because the on-call engineer assumed it was just another noisy, useless alert.
* **Burnout by 1,000 Cuts:** Being woken up at 3:00 AM is physically and mentally taxing. Waking an engineer up for a non-actionable alert is a failure of engineering management. It directly contributes to high turnover and a profound hatred of being on-call.
* **Hidden Outages:** In a sea of red dashboards and firing alerts, the critical signal (e.g., "Checkout is failing") gets buried under 50 irrelevant warnings about Redis cache evictions.

## An Operationally Sound Approach

A mature alerting philosophy is governed by a few ruthless principles:

1. **Every Page Must Be Actionable:** If an alert fires and the on-call engineer's response is to "just keep an eye on it," the alert is broken and must be deleted or tuned immediately. A page means a human must take an action *right now* to prevent or mitigate customer pain.
2. **No "Warning" Pages:** Pages are for emergencies. Warnings (e.g., "Disk is at 70%") should generate tickets for normal business hours, not wake people up.
3. **Alert on the Boundary, Not the Internals:** The customer doesn't care if your database CPU is at 99%. They care if their request timed out. We alert on what the customer experiences (latency, errors, availability), not the underlying infrastructure metrics. Infrastructure metrics are for debugging *after* the page fires.

## Decision-Making Under Pressure

The hardest decision in alerting is not what to alert on, but what *not* to alert on.

* **Delete the Noise:** It takes courage to delete an alert that has fired 50 times without requiring action. The fear is always, "What if we need it someday?" The operational reality is that the noise is a greater threat to your system's reliability than the hypothetical failure the alert was designed to catch. Delete it.
* **Continual Pruning:** Alerting is not a set-it-and-forget-it exercise. It requires constant gardening. Every postmortem must ask: "Did the right alert fire? Did any useless alerts fire? How can we tune the signal-to-noise ratio?"

Alerting is a contract with your engineers. You are promising that if you interrupt their sleep, it will be for a good reason. Respect that contract.
