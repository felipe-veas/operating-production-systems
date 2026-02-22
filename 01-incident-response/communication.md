# Incident Response: Communication

## The Information Void

During a production outage, the technical problem is only half the crisis. The other half is the information void. Customers, executives, support teams, and other engineers need to know what's happening, how bad it is, and when it will be fixed. If you don't fill that void proactively with scoped, accurate information, people will fill it with panic and constant interruptions.

## Where We Go Wrong

The default mode for engineers during an incident is to put their heads down, tail logs, and try to fix it. Communication becomes an afterthought—a hasty Slack message after an hour of silence, or a highly technical update that no one outside the team understands ("The Redis cluster OOM'd because of a bad query plan, we are tuning maxmemory-policy").

## The Cost of Poor Communication

Failing to communicate during an incident has severe operational consequences.

* **Executive Escalation:** When stakeholders don't get updates, they join the incident channel and start asking responders directly. This destroys context and delays resolution.
* **Customer Trust Erosion:** Silence on a status page while a service is down is worse than admitting a problem. Customers interpret silence as incompetence.
* **Support Team Overload:** If support doesn't know there's an ongoing incident or what to tell users, they treat every ticket as a unique issue, burning cycles and frustrating users.
* **Internal Confusion:** Other teams might waste time debugging their own systems, not realizing the root cause is a shared dependency that is currently down.

## Structured Communication

Effective incident communication requires structure, audience awareness, and a predictable cadence. It's a core responsibility of incident response, not an optional extra.

1. **The Communications Lead:** Dedicate a specific person whose sole job is translating the technical reality into actionable updates for different audiences. They interface with the Incident Commander, not the engineers deep in the code.
2. **Audience-Tailored Updates:**
    * **Internal Engineering:** Technical details, current theories, and requests for specific expertise.
    * **Executives/Stakeholders:** Business impact (e.g., "Checkout is down for 20% of users"), high-level status (Investigating vs. Mitigating), and the time of the next update. Skip the jargon.
    * **Customer Support:** What to tell customers, workarounds if any, and the time of the next update.
    * **Public Status Page:** Acknowledgment of the issue, reassurance that we're working on it, and the time of the next update. Keep it simple and honest.

## Setting a Cadence

The most critical decision regarding communication is establishing and rigidly sticking to a cadence.

* **The Promise of the Next Update:** Every single communication must end with a timestamp for the next update (e.g., "Next update in 30 minutes"). If you have no new information in 30 minutes, send an update saying exactly that: "Still investigating database latency. No new information. Next update in 30 minutes." This single practice eliminates most stakeholder anxiety.
* **Fact over Speculation:** Communicate what you know, not what you suspect. "We are seeing elevated error rates on the payment API" is better than "We think the payment provider is down." If a fix is being deployed, state that it is deploying, not that it will resolve the issue—until it actually does.

Communication isn't about having all the answers. It's about managing expectations and maintaining trust while you find those answers.
