# Alerting: SLO Alerting

## The Reality of Production Signals

Traditional alerting is binary and threshold-based: if CPU > 80% for 5 minutes, send a page. This approach is fundamentally flawed because it ignores the dimension of time and the cumulative impact on the user. A service that spikes to 90% CPU for exactly 4 minutes every hour will never trigger the alert, yet users are experiencing intermittent, severe latency. Conversely, a service might hit 81% CPU for 6 minutes during a daily batch job, triggering an alert even though users expect and tolerate that specific slowdown.

## Where Teams Go Wrong

Teams often attempt to fix noisy or inaccurate threshold alerts by adding more thresholds. They create complex, nested rules: "If CPU > 80% AND Error Rate > 2% AND Time is between 9 AM and 5 PM..." This brittle logic inevitably fails when traffic patterns change, or a new failure mode emerges that the rules didn't anticipate.

The root cause of this failure is alerting on *causes* (CPU) or instantaneous *symptoms* (current error rate) rather than the long-term reliability target: the Service Level Objective (SLO).

## The Cost of Threshold Alerting

* **The "Slow Burn" Outage:** A service that consistently fails 0.5% of requests might never trigger a static 1% error rate alert. Over a month, however, this slow burn degrades the user experience significantly and breaches the SLA with customers, completely undetected by the on-call engineer until the angry emails arrive.
* **Irrelevant Pages:** Paging an engineer at 2:00 AM because a non-critical background job caused a 5-minute spike in latency, when the service has been flawlessly fast for the previous 29 days, is a profound waste of human capital. The overall reliability over the month is still excellent.
* **Constant Tuning:** Thresholds must be constantly adjusted as traffic grows. What was a high error rate in January might be the normal background noise in November.

## An Operationally Sound Approach

Service Level Objective (SLO) based alerting, specifically **Error Budget Burn Rate Alerting**, is the industry standard for mature operational teams. It directly ties pages to customer pain and long-term reliability goals.

1. **Define the SLO:** e.g., "99.9% of checkout requests must succeed in < 500ms over a 30-day window."
2. **The Error Budget:** If you allow 0.1% of requests to fail over 30 days, that 0.1% is your error budget.
3. **Burn Rate Alerting:** Instead of alerting when the current error rate is high, you alert when you are *consuming your error budget too fast*. If you burn through 5% of your 30-day error budget in a single hour, that is a severe, actionable incident (a fast burn).

## Decision-Making Under Pressure

The shift to SLO-based alerting radically changes how teams prioritize work.

* **The "Fast Burn" (Page):** If the error budget is burning so fast that it will be exhausted in 2 days, you page the engineer immediately. This is a critical outage. The system is actively degrading customer trust at an unacceptable rate.
* **The "Slow Burn" (Ticket):** If the error budget is burning at a rate that will exhaust it in 25 days, you do not page anyone. You create a ticket for the next sprint. The team must prioritize fixing the slow leak before building new features.
* **The "No Alert" (Normal Operations):** If the error budget is burning normally, engineers are free to push code, run experiments, and deploy riskier changes. The system is within its operational boundaries.

SLO alerting is not just a monitoring technique; it is a mechanism for aligning engineering velocity with operational safety. It tells you exactly when to stop building features and start fixing reliability.
