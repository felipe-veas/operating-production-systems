# Alerting: Symptoms vs. Causes

## The Reality of Production Signals

When a user clicks "Add to Cart" and the request fails, they experience a symptom: the application is broken. Under the hood, the cause might be a database deadlock, a Redis connection timeout, a network partition, or a bad code deployment. The reality of complex systems is that a single symptom (user impact) can be triggered by dozens, if not hundreds, of different underlying causes.

## Where Teams Go Wrong

The instinct of most engineers is to alert on causes. They write a query to monitor the `cart_db` connection pool. If it exceeds 80% capacity, they fire an alert. Then they write an alert for Redis memory. Then an alert for the RabbitMQ queue length.

They attempt to enumerate every possible failure mode of their infrastructure and build an alert for it. This is a Sisyphean task. You cannot predict every way a distributed system will fail, and alerting on causes guarantees a noisy, fragile operational environment.

## The Cost of Cause-Based Alerting

* **The Alert Storm:** When a database slows down (the cause), it might trigger alerts for high CPU, high connection count, slow queries, and disk I/O. Simultaneously, the five microservices that depend on that database will fire alerts for connection timeouts, queue backups, and thread pool exhaustion. The on-call engineer receives 50 pages for a single underlying issue, making it impossible to quickly identify the root problem.
* **The Silent Failure:** Because you cannot predict every cause, you will eventually experience an outage where the system fails in a novel way. If you only alert on known causes, the system will fail silently, and you will learn about the outage from angry customers on Twitter, not your monitoring tools.
* **Brittle Configuration:** Cause-based alerts require constant tuning. If you change your database instance type, you have to update the CPU thresholds on 20 different alerts. This toil slowly degrades the quality of the monitoring.

## An Operationally Sound Approach

A mature operational model shifts entirely to **symptom-based alerting**. You alert on what the user experiences, not the health of the underlying components.

1. **The Golden Signals:** Focus alerting on Latency (how long requests take), Traffic (how much demand is on the system), Errors (rate of failed requests), and Saturation (how "full" the system is, though this borders on cause).
2. **Alert on the Boundary:** If the checkout service has a 5% error rate, that is a symptom. Page the on-call engineer. It doesn't matter *why* it's failing at 3:00 AM; it only matters that it *is* failing and requires human intervention.
3. **Dashboards are for Causes:** Once the engineer is paged for the symptom (High Error Rate), they open a dashboard to find the cause. The dashboard shows the database CPU, the Redis memory, and the queue lengths. The alert tells you *that* you are broken; the dashboard tells you *why*.

## Decision-Making Under Pressure

The shift to symptom-based alerting requires a change in how engineers investigate problems.

* **Follow the Pain, Not the Red Lights:** During an incident, ignore the noise of underlying infrastructure alerts (if they still exist). Start at the symptom (the customer impact) and work backward. "Checkout is failing. Which dependency is returning 500s? The inventory service. Why is inventory failing? Its database is locked."
* **Trust the Symptom:** If a symptom alert fires but all infrastructure metrics look fine, the problem is real. Do not dismiss an elevated error rate just because CPU is low. The user experience is the ultimate source of truth.

Symptom-based alerting drastically reduces noise, catches unknown failure modes, and aligns engineering effort with customer pain.
