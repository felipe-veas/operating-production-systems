# Incident Response: Communication

## The Information Void

During an outage, the technical failure is only half the problem. The other half is the information void. Stakeholders, support teams, and other engineers need to know the impact and the timeline. If you don't proactively fill this void with accurate updates, people fill it with panic and interrupt the responders.

## The Default Anti-Pattern

Engineers naturally default to putting their heads down, tailing logs, and trying to fix the issue. Communication becomes an afterthought. This usually results in an hour of radio silence followed by a highly technical update that stakeholders can't parse (e.g., "Redis OOM'd due to a bad query plan, tuning maxmemory-policy").

## Operational Impact of Poor Communication

Failing to communicate during an incident directly degrades the response effort:

* **Executive Interference:** When stakeholders lack updates, they drop into the incident channel and interrogate responders. This breaks focus and delays mitigation.
* **Customer Trust:** A green status page during a hard down is worse than admitting a failure. Customers view silence as incompetence.
* **Support Overload:** If support teams don't know an incident is ongoing, they treat every user report as a unique bug, wasting cycles and frustrating customers.
* **Internal Churn:** Downstream teams waste time debugging their own healthy services because they don't know a shared dependency is failing.

## Structured Communication

Incident communication requires structure and a predictable cadence. It is a core operational duty, not a nice-to-have.

1. **The Communications Lead:** Assign someone specifically to translate technical reality into actionable updates. They interface with the Incident Commander, not the engineers actively debugging.
2. **Audience-Tailored Updates:**
    * **Engineering:** Technical context, current theories, and requests for specific SMEs.
    * **Stakeholders:** Business impact ("Checkout is failing for 20% of users"), current phase (Investigating vs. Mitigating), and the time of the next update. Omit the jargon.
    * **Customer Support:** Customer-facing messaging, known workarounds, and the time of the next update.
    * **Status Page:** Acknowledgment of the issue, confirmation that teams are engaged, and the time of the next update. Keep it factual.

## Enforcing a Cadence

The most effective communication tool is a rigid update cadence.

* **The Next Update Timestamp:** Every message must end with a specific time for the next update (e.g., "Next update in 30 minutes"). If nothing changes in 30 minutes, send an update stating exactly that: "Still investigating database latency. No new findings. Next update in 30 minutes." This single habit stops stakeholders from asking for ETAs.
* **Facts Over Speculation:** State what you observe, not what you guess. "We see elevated 5xx errors on the payment API" is safer than "The payment provider is down." If you are deploying a fix, state that the deployment is in progress, not that it will solve the issue.

Communication during an incident isn't about having the root cause. It's about managing expectations and protecting the responders' cognitive load while they find it.
