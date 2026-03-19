# Operational Load: Automation

## The Limits of Human Operations

At scale, operational load outpaces human capacity. You cannot manually provision 500 database shards, rotate TLS certificates across 2,000 microservices, or SSH into a fleet of workers to restart deadlocked processes. If a production task requires execution more than three times, a human should never do it again.

## Where We Go Wrong

The failure mode isn't a refusal to automate; it's automating the wrong things, in the wrong order, using the wrong tools.

Teams fail when they treat automation as a patch for bad architecture. Writing a cron job to restart a service with a memory leak every 24 hours isn't engineering—it's hiding a fundamental flaw. They also fail by writing fragile, bespoke bash scripts that live on a single laptop. This trades manual toil for operational fragility.

## The Cost of Poor Automation

Bad automation is a liability.

* **The Automated Outage:** A script that scales down instances based on a faulty CPU metric can wipe out a production fleet in seconds. Humans make mistakes slowly; scripts make them at the speed of the CPU.
* **The Glue Code Maintenance Burden:** Thousands of lines of undocumented Python and Bash scattered across Jenkins servers and cron nodes become a maintenance nightmare. When underlying APIs change, the automation breaks silently. You usually discover this during an incident.
* **Masking Systemic Flaws:** Automating a symptom (restarting a leaky service) removes the immediate pain but allows the disease to persist. This guarantees a larger cascading failure when the automated restart inevitably breaks.

## An Operationally Sound Approach

Treat automation with the exact same rigor as product code.

1. **Automate the "Paved Road" First:** Focus on the core, repetitive tasks every team needs: CI/CD pipelines, infrastructure provisioning, certificate rotation, and standardized monitoring.
2. **Infrastructure as Code (IaC):** Define all infrastructure in code (Terraform, Pulumi), version-control it, require peer review, and apply it through an automated pipeline. No human should need SSH or console access to manually provision production resources.
3. **Test the Automation:** A database failover script is more critical than your login page. It requires tests and regular execution (e.g., via Game Days) to ensure it actually works at 3:00 AM.
4. **Fix the Root Cause:** If a service requires constant automated intervention to stay alive, fix the service. Do not improve the intervention script.

## Decision-Making

The critical decision in automation is defining the boundary of human intervention during a crisis.

* **Automate Mitigation, Require Human Investigation:** A mature system automatically mitigates failure (e.g., auto-scaling a bottleneck, circuit-breaking a failing dependency, failing over to a replica). However, it should *never* automatically close the incident. A human must investigate *why* the mitigation fired to address the underlying systemic flaw.
* **The Kill Switch:** Every piece of active automation—especially auto-scaling or automated remediation—must have a documented, accessible kill switch. If automation goes rogue during an incident, the Incident Commander must be able to disable it instantly to stop the bleeding.

Automation does not replace engineers. It provides leverage so they can focus on systemic reliability instead of repetitive chores.
