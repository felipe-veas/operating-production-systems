# Operational Load: Automation

## The Limits of Human Operations

In a modern, distributed architecture, operational scale simply outpaces human capacity. You can't manually provision 500 database shards, manually rotate TLS certificates across 2,000 microservices, or manually SSH into a fleet of workers to restart deadlocked processes. In production, if a task must be done more than three times, a human should never do it again.

## Where We Go Wrong

The failure mode with automation is rarely that teams refuse to automate; it's that they automate the wrong things, in the wrong order, using the wrong tools.

Teams fail when they treat automation as a silver bullet for bad architecture. If a service requires a manual restart every 24 hours because of a memory leak, writing a cron job to restart it isn't engineering; it's hiding a fundamental flaw. They also fail by writing fragile, bespoke bash scripts that live on a single engineer's laptop and are completely undocumented, trading manual toil for operational fragility.

## The Cost of Poor Automation

When automation is implemented poorly, it becomes a liability rather than an asset.

* **The "Automated Outage":** A poorly written script that automatically scales down instances based on a faulty CPU metric can take out the entire production fleet in seconds. When humans make mistakes, they usually make them slowly. When scripts make mistakes, they make them at the speed of the CPU.
* **The Glue Code Maintenance Burden:** Thousands of lines of undocumented Python and Bash scattered across Jenkins servers and cron nodes become a nightmare to maintain. When the API they rely on changes, the automation breaks silently, and the team discovers the failure during an incident.
* **Masking Systemic Flaws:** Automating the symptom (restarting a leaky service) removes the immediate pain but allows the disease (the memory leak) to persist, potentially cascading into a larger failure when the automated restart inevitably breaks.

## An Operationally Sound Approach

A mature automation strategy is deliberate, tested, and treated with the exact same rigor as product code.

1. **Automate the "Paved Road" First:** Focus automation on the core, repetitive tasks every team needs: CI/CD pipelines, infrastructure provisioning (Infrastructure as Code), certificate rotation, and standardized monitoring.
2. **Infrastructure as Code (IaC):** All infrastructure must be defined in code (Terraform, Pulumi, etc.), version-controlled, peer-reviewed, and applied through an automated pipeline. No human should need SSH access to production or console access to manually provision resources.
3. **Test the Automation:** A script that automatically fails over a database is more critical than the product's login page. It must have tests and be exercised regularly (e.g., via chaos engineering) to ensure it actually works when the primary database dies at 3:00 AM.
4. **Fix the Root Cause:** If a service requires constant, automated intervention to stay alive, the engineering priority is to fix the service, not improve the intervention script.

## Decision-Making

The critical decision in automation is determining the boundary of human intervention during a crisis.

* **Automate Mitigation, Require Human Investigation:** A mature system should automatically mitigate failure (e.g., auto-scaling a bottleneck, circuit-breaking a failing dependency, or failing over to a replica). However, it should *never* automatically close the incident. A human must always investigate *why* the automated mitigation fired to ensure the underlying systemic flaw is addressed.
* **The Kill Switch:** Every piece of active automation (especially auto-scaling or automated remediation) must have a clearly documented, easily accessible kill switch. If the automation goes rogue during an incident, the Incident Commander must be able to disable it instantly to stop the bleeding.

Automation isn't about replacing engineers; it's about elevating their leverage so they can focus on systemic reliability work instead of repetitive chores.
