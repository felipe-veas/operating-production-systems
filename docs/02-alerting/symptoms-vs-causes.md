# Alerting: Symptoms vs. Causes

## Production Realities

When a user clicks "Add to Cart" and the request fails, they experience a symptom. The underlying cause could be a database deadlock, a Redis timeout, a network partition, or a bad deployment. In distributed systems, a single symptom (user impact) can stem from hundreds of different causes.

## Common Anti-Patterns

Engineers instinctively alert on causes. They monitor the `cart_db` connection pool and alert at 80%. They add alerts for Redis memory and RabbitMQ queue depth.

Trying to enumerate every possible failure mode is impossible. Alerting on causes guarantees a noisy, fragile operational environment.

## Operational Impact

Relying on cause-based alerts creates chaos during incidents:

* **The Alert Storm:** A slow database triggers alerts for CPU, connections, and disk I/O. Meanwhile, five dependent microservices fire alerts for timeouts and queue backups. The on-call engineer gets 50 pages for one issue, burying the root cause.
* **The Silent Failure:** You can't predict every cause. When the system fails in a novel way, known-cause alerts stay green. You find out about the outage from Twitter, not your monitoring tools.
* **Brittle Configuration:** Cause-based alerts require endless tuning. Upgrading a database instance means updating CPU thresholds across 20 alerts. This toil degrades monitoring quality.

## Operational Standards

A mature operational model shifts entirely to **symptom-based alerting**. Alert on what the user experiences, not the health of underlying components.

1. **The Golden Signals:** Focus alerting on Latency (how long requests take), Traffic (demand on the system), Errors (rate of failed requests), and Saturation (how "full" the system is).
2. **Alert on the Boundary:** A 5% error rate on checkout is a symptom. Page the engineer. It doesn't matter *why* it's failing at 3:00 AM; it only matters that it *is* failing and requires intervention.
3. **Dashboards are for Causes:** Alerts tell you *that* you are broken; dashboards tell you *why*. Once paged for a symptom, open a dashboard to check database CPU, Redis memory, or queue lengths.

## Incident Investigation

Symptom-based alerting changes how engineers investigate problems.

* **Follow the Pain, Not the Red Lights:** During an incident, ignore infrastructure noise. Start at the customer impact and work backward: "Checkout is failing. Which dependency is returning 500s? The inventory service. Why is inventory failing? Its database is locked."
* **Trust the Symptom:** If a symptom alert fires but infrastructure metrics look fine, the problem is still real. Don't dismiss an elevated error rate just because CPU is low. User experience is the ground truth.

Symptom-based alerting drastically reduces noise, catches unknown failure modes, and aligns engineering effort with actual customer pain.
