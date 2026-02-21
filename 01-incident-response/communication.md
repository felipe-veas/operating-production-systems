# Incident Response: Communication

## The Reality of Production Outages

When a production system fails, the technical reality is only one facet of the crisis. The other is the information void. Customers, executives, support teams, and other engineering squads all need to know what is happening, how bad it is, and when it will be fixed. If that void isn't filled proactively with accurate and appropriately scoped information, people will fill it with panic, speculation, and constant interruptions to the responders.

## Where Teams Go Wrong

The default mode for engineers during an incident is to put their heads down, look at logs, and try to fix the problem. Communication becomes an afterthought—a hasty Slack message after an hour of silence, or a highly technical update that no one outside the team understands ("The Redis cluster OOM'd because of a bad query plan, we are tuning maxmemory-policy").

## The Cost of Ad-Hoc Heroics

Poor communication during an incident has severe operational consequences.

* **Stakeholder Anxiety and Escalation:** When executives don't get updates, they join the incident channel and start asking the responders directly. This destroys the responders' context and significantly delays resolution.
* **Customer Trust Erosion:** Silence on a public status page while a service is down is worse than admitting a problem. Customers interpret silence as incompetence or apathy.
* **Support Team Overwhelm:** If customer support doesn't know there's an ongoing incident or what to tell users, they are forced to investigate every ticket as a unique issue, burning cycles and frustrating customers.
* **Internal Confusion:** Other engineering teams might waste time debugging their own systems, not realizing the root cause is a shared dependency that is currently down.

## An Operationally Sound Approach

Effective incident communication requires deliberate structure, audience awareness, and a predictable cadence. It is a core responsibility of incident response, not an optional extra.

1. **The Communication Lead:** Dedicate a specific person (often called the Communications Lead or Incident Communicator) whose sole job is to translate the technical reality into clear, actionable updates for different audiences. They interface with the Incident Commander, not the engineers deep in the code.
2. **Audience-Tailored Updates:**
    * **Internal Engineering:** Technical details, current theories, and requests for specific expertise.
    * **Executives/Stakeholders:** Business impact (e.g., "Checkout is down for 20% of users"), high-level status (Investigating vs. Mitigating), and the time of the next update. No technical jargon.
    * **Customer Support:** What to tell customers, workarounds if any, and the time of the next update.
    * **Public Status Page:** Acknowledgment of the issue, reassurance that it's being worked on, and the time of the next update. Keep it simple and honest.

## Decision-Making Under Pressure

The most critical decision regarding communication is establishing and rigidly adhering to a cadence.

* **The Promise of the Next Update:** Every single communication, internal or external, must end with a timestamp for the next update (e.g., "Next update in 30 minutes"). If you have no new information in 30 minutes, you send an update saying exactly that: "We are still investigating the database latency. No new information. Next update in 30 minutes." This single practice eliminates 90% of stakeholder anxiety.
* **Fact over Speculation:** Communicate what is known, not what is suspected. "We are seeing elevated error rates on the payment API" is better than "We think the payment provider is down." If a fix is being deployed, state that it is being deployed, not that it will resolve the issue until it actually has.

Communication is not about having all the answers; it's about managing expectations and maintaining trust while the answers are being found.
