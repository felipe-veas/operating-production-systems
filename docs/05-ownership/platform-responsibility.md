# Ownership: Platform Responsibility

## The Platform Boundary

As engineering organizations scale, having every product team manage their own Kubernetes clusters, CI/CD pipelines, and databases becomes inefficient and risky. The standard solution is a Platform (or Infrastructure/SRE) team that provides these capabilities as internal products. However, the boundary between the platform and the applications running on it frequently causes friction, outages, and organizational dysfunction.

## Where We Go Wrong

Platform engineering usually fails when responsibilities are poorly defined.

Product teams often treat the platform as magic. When an application goes down, the instinct is to blame the infrastructure: "Kubernetes is broken," "The network dropped packets," or "The database is slow." They stop trying to understand how their code interacts with the underlying systems.

Conversely, Platform teams often build in a vacuum, prioritizing technical elegance over developer experience. They mandate complex pipelines without providing documentation, support, or self-service escape hatches. When product teams struggle, Platform blames "developer incompetence."

## The Cost of Blurred Boundaries

When the line between application and platform becomes adversarial, the organization suffers.

* **The "Not My Problem" Outage:** An application starts OOM-killing. The product team blames Kubernetes resource limits; the platform team blames an application memory leak. While they argue in Slack, the system stays down.
* **Platform as a Bottleneck:** If developers need a Jira ticket to provision a database, the Platform team becomes a blocker. The platform turns into a bureaucracy rather than an accelerator.
* **Shadow IT:** Frustrated developers will bypass the platform entirely, spinning up rogue AWS accounts or unauthorized SaaS tools. The organization loses control over security, compliance, and infrastructure spend.

## An Operationally Sound Approach

A mature Platform team operates like an internal SaaS provider. They build products for their customers (developers), with boundaries explicitly defined by Service Level Agreements (SLAs).

1. **Platform as a Product:** Treat the platform like an external vendor. It requires clear documentation, a defined API (Infrastructure as Code), and guaranteed uptime. If the platform provides a database-as-a-service, the platform team owns its uptime, backups, and patching.
2. **Explicit Contracts:** The boundary between platform and application is a contract. The platform guarantees compute, network, and storage. The application guarantees it will implement health checks, handle retries, manage its memory, and respect rate limits. If the platform is healthy but the application is crashing, the product team owns the incident.
3. **Self-Service is Mandatory:** A Platform team's success is measured by how rarely developers need to talk to them. Provisioning resources, deploying code, and accessing logs must be fully automated and self-service.

## Decision-Making

Managing platform responsibility comes down to handling incidents at the boundary.

* **Boundary Postmortems:** When an incident spans both layers (e.g., a bad deployment script takes down a cluster), the postmortem must focus on the interface. Why did the platform allow an application to exhaust cluster resources? Why didn't the application use circuit breakers? Fix the resilience of the boundary.
* **The Golden Path:** The platform team defines a "Golden Path"—a fully supported, automated stack. If a product team deviates (e.g., running an unsupported graph database), they explicitly accept full operational responsibility. The platform team does not carry the pager for bespoke choices.

A successful platform is invisible when it works and unambiguously accountable when it fails. It removes toil, not responsibility.
