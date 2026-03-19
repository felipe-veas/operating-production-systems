# Principles: Reliability Principles

## The Physics of Distributed Systems

At scale, the probability of failure approaches 100%. You can't buy reliability with expensive hardware or the latest orchestrator. Reliability is an emergent property of system design, testing, and operational response.

## Core Principles

These aren't aspirational goals; they are operational realities.

1. **Failure is Inevitable:** Hardware degrades. Networks partition. Dependencies return 500s. If your architecture assumes all components are healthy, it's already broken.
2. **MTTR > MTBF:** You can't prevent every outage. Optimize for recovery (MTTR) over time between failures (MTBF). A system that fails daily but recovers in seconds is better than one that fails yearly but takes days to rebuild.
3. **Complexity is the Enemy:** Every new microservice, queue, or abstraction is a new failure domain. Only add complexity when the business value clearly outweighs the operational tax. Boring technology is reliable technology.
4. **Graceful Degradation:** If the recommendation engine fails, users must still be able to check out. Design systems to fail partially. Shed non-critical features to protect the core business flow.

## Architectural Anti-Patterns

When teams ignore these principles, they build fragile architectures that collapse under their own weight.

* **Cascading Failures:** A minor database slowdown backs up a queue, OOM-kills a microservice, and forces the API gateway to drop connections. Without bulkheads and circuit breakers, localized latency becomes a platform-wide SEV1.
* **The Impossible SLA:** Promising 99.99% uptime on a service that relies on a third-party API with a 99.9% SLA is mathematically impossible. You cannot be more reliable than your critical dependencies without fallback mechanisms.

## Resilience Patterns

Reliability engineering is the active mitigation of risk through deliberate design.

* **Design for Retries and Idempotency:** Network calls fail. Services must retry safely. Downstream endpoints must be idempotent to handle duplicate requests without corrupting data during a retry storm.
* **Timeouts and Circuit Breakers:** Never wait indefinitely for a response. Enforce strict timeouts. If a dependency degrades, open a circuit breaker to halt traffic, allowing the dependency to recover and preventing thread exhaustion in your own service.
* **Defense in Depth:** Don't rely on a single safety mechanism. Combine rate limiting for traffic spikes, strict input validation, and automated rollbacks for bad deployments.

Reliability is the continuous management of risk and complexity.
