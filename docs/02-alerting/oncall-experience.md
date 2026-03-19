# Alerting: On-Call Experience

## Production Realities

On-call is where code meets production. For the engineer holding the pager, it means disrupted sleep, restricted personal time, and the anxiety of fixing unfamiliar systems under pressure.

## Common Anti-Patterns

Management often treats on-call as an unavoidable tax on engineering—a hazing ritual rather than a core business function. Teams fail by ignoring the human cost: they don't track off-hours wake-ups, they ignore the time wasted on unactionable alerts, and they offer zero compensation for disrupted lives.

## Operational Impact

A hostile on-call environment degrades the entire engineering organization:

* **Burnout and Attrition:** Engineers will quit over a toxic rotation. The institutional knowledge lost when a senior engineer burns out is massive and expensive to replace.
* **Fear-Driven Development:** Engineers terrified of the pager become overly cautious. They over-engineer solutions, delay deployments, and avoid owning complex systems. Velocity stalls.
* **The "Hero" Anti-Pattern:** A brutal rotation forces a few senior "heroes" to bear the burden because they hold all the undocumented context. This masks architectural fragility and creates human single points of failure.

## Operational Standards

A sustainable rotation requires treating the health of the on-call engineer as a critical operational metric, right alongside uptime.

1. **Sustainable Rotations:** Require at least 6 engineers per rotation. Anything less means individuals are on-call too frequently, preventing recovery between shifts.
2. **Compensation and Time Off:** On-call restricts freedom even when the pager is quiet. Compensate for this with money or guaranteed time off (e.g., a mandatory recovery day after a severe incident).
3. **The "Fix It" Rotation:** An on-call engineer's primary job is responding to pages. Their secondary job is fixing what paged them. Shield them entirely from sprint work and feature development during their shift.

## Leadership Responsibilities

Managing the on-call experience requires active intervention from engineering leadership.

* **Protecting the Team:** If a service is inherently unstable and paging constantly, management must halt feature development on that service until reliability improves. You cannot build a sustainable product on burning engineers.
* **Blameless Escalation:** Explicitly encourage early escalation. Engineers shouldn't hesitate to wake a senior colleague if they're stuck. A toxic culture punishes escalation; a healthy culture praises engineers for recognizing their limits and prioritizing system recovery.

The goal isn't to eliminate on-call, but to make it boring and predictable. A quiet rotation is the ultimate metric of operational maturity.
