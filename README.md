# Operating Production Systems

This repository contains an opinionated, experience-driven set of principles and practices for operating software systems at scale.

It is not a tutorial on Kubernetes, a configuration guide for Datadog, or an academic treatise on distributed systems. Instead, it is a reflection of what actually breaks in production, how teams behave under pressure, and how reliability is systematically improved over time.

The content here is written for senior engineers, hiring managers, and platform/SRE teams. It focuses on:

- Tradeoffs in system design and operational models.
- Operational risk and human factors.
- Coordination, escalation, and decision-making during incidents.

## Structure

The documentation is organized by core operational domains:

- **[01. Incident Response](./01-incident-response/)**: Structuring chaos, managing severity, and effective coordination.
- **[02. Alerting](./02-alerting/)**: Designing actionable signals, preventing alert fatigue, and focusing on symptoms over causes.
- **[03. Postmortems](./03-postmortems/)**: Extracting organizational learning through blameless investigations and rigorous action items.
- **[04. Operational Load](./04-operational-load/)**: Managing toil, tribal knowledge, and ensuring a sustainable on-call experience.
- **[05. Ownership](./05-ownership/)**: Defining boundaries, navigating developer vs. operations dynamics, and building a production-first culture.
- **[99. Principles](./99-principles/)**: Core engineering values and operational safety principles that underline everything else.

## Philosophy

Reliability is not a product you can buy or a tool you can deploy. It is a property of the socio-technical system—the combination of software, infrastructure, and the humans who operate them.

Tools change. Cloud providers change. But the fundamental challenges of operating complex systems—coordinating humans, defining boundaries, maintaining psychological safety, and managing risk—remain constant.
