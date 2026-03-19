# Postmortems: Organizational Learning

## The Silo Problem

When an engineering team experiences a catastrophic outage, investigates it rigorously, and implements robust action items, that specific team becomes marginally more reliable. But in a growing organization, the lessons learned by one squad rarely propagate to the others. The knowledge gained from a SEV1 incident stays trapped within the silos of the responders.

Most organizations treat postmortems as localized events. The incident commander writes the document, the affected team reviews it, action items go onto their specific Jira board, and the document is archived in a wiki that no one outside the team ever reads.

## The Cost of Hidden Context

Failing to learn at an organizational level is expensive. It guarantees repeated outages. Team A discovers a fundamental flaw in how the message broker handles network partitions. Six months later, Team B builds a new service using the same message broker, ignorant of the flaw, and experiences the exact same outage.

The forensic investigation of a complex failure provides highly valuable engineering context. When hidden, the organization's collective intelligence remains static. An engineering department might write 50 postmortems a year, but if lessons aren't shared, the organization isn't maturing—it's just failing frequently and locally.

## Distributing Knowledge

A mature engineering culture requires explicit mechanisms for distributing knowledge gained from failure across the entire organization.

1. **Hold public postmortem reviews:** Every SEV1 and significant SEV2 incident must be reviewed in a recurring, open-invitation meeting. This isn't a status update; it's an engineering presentation. The team presents the timeline, the root causes, and the systemic fixes they are implementing.
2. **Curate the failures:** The SRE or Platform team should curate the most widely applicable postmortems into regular communication, such as a dedicated Slack channel or a segment in the engineering all-hands.
3. **Identify macro-patterns:** The ultimate goal is identifying trends across incidents. Are 40% of outages related to bad database migrations? Are we consistently missing latency alerts? The SRE team's highest-leverage work is identifying these patterns and prioritizing cross-team engineering initiatives to fix them.

## Leadership's Role

Fostering organizational learning means prioritizing transparency over ego. When an engineering leader stands up in an all-hands, describes a massive outage their team caused, and explains exactly how they fixed the systemic vulnerability, it sets the standard. It demonstrates that failure is expected, investigated deeply, and shared openly.

Furthermore, if a postmortem reveals a flaw in a shared infrastructure component, leadership must prioritize fixing the shared component (the "paved road") rather than requiring every individual service owner to implement their own local workaround.

Organizational learning is the compounding interest of reliability. Every failure, properly investigated and widely shared, makes the entire system more resilient.
