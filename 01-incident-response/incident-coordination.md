# Incident Response: Incident Coordination

## The Human Problem

During a critical production incident, the technical problem is only half the battle. The other half is human coordination. When a core service goes down, engineers from multiple teams, DBAs, and customer support converge in a chaotic digital space. Information scatters across Slack threads, Zoom chats, and Jira tickets. The sheer volume of incoming data and the pressure to resolve the issue quickly create a highly volatile environment.

## The Hero Anti-Pattern

The most common failure mode in incident response is the "hero" anti-pattern: a single engineer, or a small group, attempting to investigate the issue, write the fix, deploy it, and simultaneously communicate updates to stakeholders. This inevitably creates a bottleneck. When an engineer is deep in logs trying to understand why a pod is crash-looping, they can't also write a coherent status update for the VP of Engineering.

## The Cost of Fragmentation

When coordination fails, the response effort fragments.

* **Duplicate Effort:** Multiple engineers might independently investigate the same theory, wasting precious time.
* **Conflicting Actions:** One engineer might restart a database while another tries to capture a memory dump, destroying the evidence needed for root cause analysis.
* **Stakeholder Anxiety:** Without centralized communication, executives and support teams will interrupt the engineers trying to fix the problem, further delaying resolution.
* **Loss of Context:** When the "hero" finally goes to sleep, the next shift has no record of what was tried, what failed, and what the current theories are.

## An Operationally Sound Approach

Effective coordination requires abandoning the idea that technical skill alone solves incidents. It requires adopting an Incident Command System (ICS), adapted for software engineering. The core principle is the explicit separation of roles.

1. **The Incident Commander (IC):** The IC is the single source of truth and authority. They don't write code, they don't look at dashboards, and they don't touch production. Their sole job is to maintain situational awareness, assign tasks, and keep the response organized. They ask: "What's our current theory? Who is validating it? When do we expect an update?"
2. **The Scribe:** Documents the incident timeline in real-time. This is critical for the postmortem and for handing off context to new responders.
3. **The Communicator:** Handles all external communications (status pages, executive summaries), shielding the IC and engineers from interruptions.
4. **The Responders (SMEs):** The Subject Matter Experts investigating and implementing fixes. They report *only* to the IC.

## Managing Cognitive Load

The IC must relentlessly manage cognitive load and enforce discipline. The most critical decisions an IC makes are often about what *not* to do.

* **Mitigation over Investigation:** The IC must aggressively pivot the team towards mitigating customer impact (e.g., rolling back a deploy, scaling up resources) rather than spending hours hunting for the perfect root cause while the system burns.
* **Controlling the Narrative:** The IC ensures all actions in production are explicitly authorized and communicated before execution. "I am going to restart the database now. Does anyone have concerns?"

Coordination isn't about micromanaging engineers; it's about providing the structure necessary for them to operate safely under extreme pressure.
