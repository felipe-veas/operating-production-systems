# Alerting: On-Call Experience

## The Reality of Production Operations

Being on-call is the crucible of software engineering. It's when abstract code and theoretical architecture collide with the harsh reality of production. For the engineer holding the pager, it's a period of heightened anxiety, disrupted sleep, and the underlying fear that the phone will ring and they'll be solely responsible for fixing a system they only partially understand.

## Where We Go Wrong

The most common failure mode in managing the on-call rotation is treating it as an unavoidable hazing ritual. Management often views on-call as a purely operational necessity—a tax paid by engineers for the privilege of writing code.

Teams fail because they don't actively manage the human cost. They don't track how often people are woken up. They don't measure the time spent resolving unactionable alerts. They don't provide adequate compensation (time or money) for the disruption to personal lives.

## The Cost of a Hostile On-Call Environment

When the on-call experience is brutal, the consequences extend far beyond the individual engineer's misery.

* **Burnout and Attrition:** This is the most direct and expensive consequence. Engineers will leave companies specifically because the on-call rotation is toxic. The institutional knowledge lost when a senior engineer burns out is often immeasurable.
* **Fear-Driven Development:** When an engineer is terrified of being paged for their own code, they become overly cautious. They over-engineer solutions, delay deployments, and avoid taking ownership of complex systems. Innovation stagnates.
* **The "Hero" Anti-Pattern:** A hostile on-call environment breeds a culture where a few senior engineers (the "heroes") disproportionately bear the burden because they're the only ones who know how to fix undocumented systems. This masks the underlying fragility of the architecture and creates single points of failure.

## An Operationally Sound Approach

A sustainable on-call rotation requires a fundamental shift in perspective: the health of the on-call engineer is a critical operational metric, just like system uptime.

1. **Sustainable Rotations:** A minimum of 6 engineers per rotation is required for long-term sustainability. Anything less means individuals are on-call too frequently, preventing them from recovering from the stress.
2. **Compensation and Time Off:** On-call is work, even when the pager doesn't ring. It restricts an engineer's freedom. Companies must compensate for this, either financially or with guaranteed time off (e.g., a mandatory "recovery day" after a severe incident or a particularly brutal week).
3. **The "Fix It" Rotation:** When an engineer is on-call, their primary job is responding to pages. Their secondary job is fixing the things that paged them. They should be shielded from sprint work and feature development during their rotation.

## Decision-Making Under Pressure

Managing the on-call experience requires continuous, empathetic leadership from engineering managers.

* **Protecting the Team:** If a service is inherently unstable and paging constantly, management must have the authority to pause feature development on that service until the reliability issues are addressed. You cannot build a sustainable product on a foundation of burning engineers.
* **Blameless Escalation:** The culture must explicitly encourage early escalation. An engineer should never feel ashamed to wake up a senior colleague if they're stuck. A toxic culture punishes the engineer for escalating; a healthy culture praises them for recognizing their limits and prioritizing system recovery.

The goal isn't to eliminate on-call, but to make it boring, predictable, and manageable. A quiet rotation is the ultimate metric of operational maturity.
