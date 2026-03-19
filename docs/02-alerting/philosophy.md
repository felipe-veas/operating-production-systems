# Alerting: Philosophy

## Production Realities

In distributed systems, something is always failing. Nodes recycle, networks drop packets, and background queues temporarily back up. Raw telemetry is inherently noisy. The goal of an alerting system isn't to report every anomaly—it's to extract actionable signal and demand human attention only when the system cannot heal itself and customer pain is imminent.

## Common Anti-Patterns

Teams often build alerts bottom-up. An engineer writes a microservice, adds a CPU metric, and alerts if it crosses 80%. They add alerts for memory usage, pod restarts, and slow database queries. They treat alerts as debugging tools rather than operational triggers.

## Operational Impact

A flawed alerting philosophy is toxic to engineering culture:

* **Ignored Signals:** When 90% of pages require no action (e.g., "CPU spiked for 2 minutes and recovered"), engineers learn to ignore the pager. When a real failure happens, the response is delayed because the on-call engineer assumed it was just more noise.
* **Burnout by 1,000 Cuts:** Waking an engineer at 3:00 AM for a non-actionable alert is a management failure. It directly drives turnover and makes people hate being on-call.
* **Hidden Outages:** Critical signals (e.g., "Checkout is failing") get buried under dozens of irrelevant warnings about Redis cache evictions.

## Operational Standards

A mature alerting philosophy relies on a few ruthless principles:

1. **Every Page Must Be Actionable:** If an alert fires and the response is "let's keep an eye on it," the alert is broken. A page means a human must take action *right now* to mitigate customer pain.
2. **No "Warning" Pages:** Pages are for emergencies. Warnings (e.g., "Disk at 70%") should generate tickets for normal business hours, not wake people up.
3. **Alert on the Boundary, Not the Internals:** Customers don't care if your database CPU is at 99%. They care if their request timed out. Alert on what the customer experiences (latency, errors, availability). Use infrastructure metrics for debugging *after* the page fires.

## Prioritizing Signal

The hardest decision in alerting is not what to alert on, but what *not* to alert on.

* **Delete the Noise:** It takes courage to delete an alert that fires constantly, out of fear you might need it someday. But operational noise is a greater threat to reliability than the hypothetical failure the alert was designed to catch. Delete it.
* **Continual Pruning:** Alerting requires constant gardening. Every postmortem must ask: Did the right alert fire? Did useless alerts fire? How do we improve the signal-to-noise ratio?

Alerting is a contract with your engineers. You are promising that if you interrupt their sleep, it's for a good reason. Respect that contract.
