# Incident Response: Incident Coordination

## The Human Factor

During a SEV1, the technical failure is secondary to the coordination problem. When a core service drops, engineers, DBAs, and support staff flood into a chaotic digital space. Context scatters across Slack threads, Zoom calls, and Jira tickets. The sheer volume of noise and the pressure to mitigate create a volatile environment where mistakes compound.

## The Hero Anti-Pattern

The most common failure mode is the "hero" anti-pattern: a single engineer trying to debug the issue, write a hotfix, deploy it, and update stakeholders simultaneously. This guarantees a bottleneck. An engineer deep in `kubectl` logs cannot write a coherent status update for the VP of Engineering.

## The Cost of Uncoordinated Response

When coordination breaks down, the response fragments:

* **Duplicate Effort:** Multiple responders investigate the same dead end, burning time.
* **Conflicting State Changes:** One engineer restarts a database while another tries to pull a memory dump, destroying the state needed for root cause analysis.
* **Stakeholder Interference:** Without a dedicated communicator, executives interrupt the responders directly, breaking their focus and delaying mitigation.
* **Context Loss:** When the primary responder hands off or logs off, there is no record of what was tried, what failed, and what theories remain.

## Structured Incident Command

Technical skill alone does not resolve major incidents. You need an Incident Command System (ICS) adapted for engineering. The core mechanism is the strict separation of roles.

1. **The Incident Commander (IC):** The IC holds ultimate authority over the response. They do not write code, query logs, or touch production. Their job is to maintain state, assign tasks, and drive the response forward. They ask: "What is the current theory? Who is validating it? When do we expect a result?"
2. **The Scribe:** Maintains the real-time timeline. This is mandatory for the postmortem and for onboarding new responders mid-incident.
3. **The Communications Lead:** Owns all external messaging (status pages, executive updates). They shield the IC and the responders from stakeholder noise.
4. **The Responders (SMEs):** The engineers actively debugging and executing fixes. They take direction exclusively from the IC.

## Managing Cognitive Load

The IC's primary job is managing the team's cognitive load. The most important decisions are often about what *not* to do.

* **Mitigation Over Investigation:** The IC must force the team to prioritize mitigating impact (e.g., rolling back, scaling up, failing over) rather than hunting for the root cause while the system burns.
* **State Control:** The IC ensures no one mutates production state without explicit authorization. Every action must be announced and acknowledged: "I am restarting the primary database now. Does anyone object?"

Coordination is not micromanagement. It is the framework that allows engineers to operate safely and predictably under extreme pressure.
