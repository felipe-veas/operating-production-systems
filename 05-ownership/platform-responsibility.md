# Ownership: Platform Responsibility

## The Reality of Production Boundaries

As an engineering organization scales, it becomes inefficient and dangerous for every product team to independently manage their own Kubernetes clusters, CI/CD pipelines, database backups, and network routing. The solution is the Platform (or Infrastructure/SRE) team: a centralized group that provides these foundational capabilities as internal products. However, the reality of a platform architecture is that the boundary between the platform and the application running on it is the most frequent source of friction, outages, and organizational dysfunction.

## Where Teams Go Wrong

The failure mode in platform engineering is almost always a failure of defined responsibility.

Product teams often treat the platform as a magical abstraction layer. When their application goes down, their first instinct is to blame the platform: "Kubernetes is broken," "The network dropped my packets," "The database is slow." They abdicate responsibility for understanding how their code interacts with the underlying infrastructure.

Conversely, Platform teams often build tools in a vacuum, focusing on technical elegance rather than developer experience. They mandate adoption of complex, fragile deployment pipelines without providing adequate documentation, support, or self-service escape hatches. When the product team fails to use the platform correctly, the Platform team blames "developer incompetence."

## The Cost of Undefined Platform Boundaries

When the line between application and platform is blurred or adversarial, the entire organization suffers.

* **The "Not My Problem" Outage:** An incident occurs where the application is OOM-killing. The product team says it's a Kubernetes resource limit issue; the platform team says it's an application memory leak. While they argue in Slack, the customer experiences downtime.
* **Platform as a Bottleneck:** If developers cannot self-serve (e.g., they need to open a Jira ticket to get a new database provisioned), the Platform team becomes a blocker to product velocity. The platform is no longer an accelerator; it is a bureaucracy.
* **Shadow IT:** Frustrated developers will simply bypass the platform, spinning up their own AWS accounts or using unauthorized third-party SaaS tools. The organization loses control over security, compliance, and cost.

## An Operationally Sound Approach

A mature Platform team operates as an internal SaaS provider. They build products (the platform) for their customers (the developers), and the boundary of responsibility is explicitly defined by a Service Level Agreement (SLA).

1. **The Platform as a Product:** The platform must be treated like any external vendor. It must have clear documentation, a defined API (Infrastructure as Code), and guaranteed uptime (SLAs). If the platform team provides a database-as-a-service, they own the uptime, backups, and patching of that database.
2. **Explicit Contracts:** The boundary between platform and application is a contract. The platform promises to provide compute, network, and storage. The application promises to implement health checks, handle retries, manage its own memory, and respect rate limits. If the platform is up and the application is crashing, it is the product team's incident to resolve.
3. **Self-Service is Mandatory:** The primary metric of a Platform team's success is how rarely developers need to speak to them to get their work done. Provisioning resources, deploying code, and accessing logs must be entirely self-service and automated.

## Decision-Making Under Pressure

The critical decision in managing platform responsibility is how incidents at the boundary are handled.

* **The Blameless Postmortem of the Boundary:** When an incident occurs that spans the application and the platform (e.g., a bad deployment script causes a cluster-wide failure), the postmortem must focus on the boundary itself. Why did the platform allow the application to take down the cluster? Why didn't the application have circuit breakers? The action items must improve the resilience of the interface between the two.
* **The "Golden Path" vs. "Supported Path":** The platform team must define a "Golden Path"—a highly supported, fully automated stack that product teams are encouraged to use. If a team chooses to deviate from the Golden Path (e.g., they want to run a bespoke, unsupported database), they explicitly accept full operational responsibility for it. The platform team will not hold the pager for it.

A successful platform is invisible when it works and unambiguously accountable when it fails. It empowers developers by removing toil, not by removing responsibility.
