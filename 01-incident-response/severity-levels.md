# Incident Response: Severity Levels

## Measuring Impact

When an alert triggers or a customer reports a problem, the first question is: *How bad is this?* In production, impact is rarely binary. A single endpoint timing out on a non-critical internal dashboard is vastly different from the checkout flow returning 500s for all users on Black Friday. The challenge is quantifying this impact consistently under pressure.

## Where We Go Wrong

Most organizations operate with subjective, emotionally driven severity levels. If a VP notices a typo on the homepage, it suddenly becomes a "SEV1". Conversely, a silent failure in a background job failing to process refunds might be ignored for days because no one is screaming about it. Teams fail when their severity matrix relies on technical symptoms (e.g., "The database is down") rather than business impact.

## The Cost of Misalignment

When severity is misaligned, the consequences are immediate.

* **Alert Fatigue:** If everything is treated as a critical emergency, engineers stop taking real emergencies seriously. Being paged at 3:00 AM for a SEV1 that turns out to be a minor log-parsing error destroys morale.
* **Wasted Resources:** Calling an all-hands response for a minor issue pulls people away from feature work and kills velocity.
* **Missed SLAs:** Under-classifying an incident means the right people aren't engaged fast enough, leading to breached Service Level Agreements (SLAs) and lost customer trust.

## Objective Severity

Severity levels must be objective, deterministic, and strictly tied to customer or business impact. The definitions should leave no room for interpretation.

* **SEV1 (Critical):** Core business flow is completely broken for a significant percentage of users. No workaround exists. Revenue or reputation is actively burning (e.g., "Checkout is failing for >10% of users"). Requires immediate, 24/7 all-hands response.
* **SEV2 (High):** Significant degradation of a core feature, but a workaround exists, or only a small subset of users is affected (e.g., "Password resets are delayed by 30 minutes"). Requires immediate response during business hours, paging primary on-call off-hours.
* **SEV3 (Medium):** Minor feature is broken or internal tooling is degraded. No immediate customer impact (e.g., "Internal analytics dashboard is stale"). Addressed during normal business hours via ticket.
* **SEV4 (Low):** Minor bugs, typos, or cosmetic issues. Backlog item.

## Defining Severity Under Pressure

The decision of what severity to assign must happen in the first 5 minutes of an incident. It shouldn't require a debate. If there's ambiguity, the standard procedure is to *escalate the severity initially, and downgrade later once the impact is clarified*.

Do not base severity on the difficulty of the fix. A single missing comma that breaks the entire site is a SEV1. A complex database corruption that only affects a deprecated feature no one uses is a SEV3. Severity is about the pain the customer feels, not the pain the engineer feels fixing it.
