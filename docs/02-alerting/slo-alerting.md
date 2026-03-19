# Alerting: SLO Alerting

## Production Realities

Traditional alerting is binary and threshold-based: if `CPU > 80% for 5m`, send a page. This ignores cumulative user impact. A service that spikes to 90% CPU for exactly 4 minutes every hour never triggers the alert, yet users suffer intermittent, severe latency. Conversely, a daily batch job hitting 81% CPU for 6 minutes triggers a useless page for an expected slowdown.

## Common Anti-Patterns

Teams often try to fix noisy thresholds with complex, nested rules: "If CPU > 80% AND Error Rate > 2% AND Time is 9-5..." This brittle logic breaks as soon as traffic patterns shift or new failure modes emerge.

The core mistake is alerting on *causes* (CPU) or instantaneous *symptoms* (current error rate) instead of long-term reliability targets: Service Level Objectives (SLOs).

## Operational Impact

Relying on static thresholds creates blind spots and noise:

* **The "Slow Burn" Outage:** A service failing 0.5% of requests never trips a static 1% error rate alert. Over a month, this slow burn breaches SLAs and degrades user trust, completely undetected until customers complain.
* **Irrelevant Pages:** Paging someone at 2:00 AM for a 5-minute latency spike caused by a background job—when the service was flawless for 29 days prior—wastes human capital. Overall reliability is still fine.
* **Constant Tuning:** Static thresholds require endless tweaking as traffic scales. January's high error rate becomes November's baseline noise.

## Operational Standards

SLO-based alerting, specifically **Error Budget Burn Rate Alerting**, ties pages directly to customer pain and long-term reliability.

1. **Define the SLO:** e.g., "99.9% of checkout requests must succeed in < 500ms over a 30-day window."
2. **The Error Budget:** If you allow 0.1% of requests to fail over 30 days, that 0.1% is your error budget.
3. **Burn Rate Alerting:** Alert when you consume the error budget too fast, not when the instantaneous error rate is high. Burning 5% of a 30-day budget in one hour is a fast burn and an actionable incident.

## Prioritizing Work

SLO alerting radically changes how teams prioritize reliability versus feature work.

* **The "Fast Burn" (Page):** If the budget is burning so fast it will exhaust in 2 days, page immediately. This is a critical outage actively degrading customer trust.
* **The "Slow Burn" (Ticket):** If the budget will exhaust in 25 days, do not page. Create a ticket for the next sprint. The team must fix the slow leak before building new features.
* **The "No Alert" (Normal Operations):** If the burn rate is normal, engineers are free to push code and deploy riskier changes. The system is within its operational boundaries.

SLO alerting isn't just a monitoring technique; it's a mechanism for aligning engineering velocity with operational safety. It tells you exactly when to stop shipping features and start fixing reliability.
