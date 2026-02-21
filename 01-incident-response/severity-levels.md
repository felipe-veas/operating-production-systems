# Incident Response: Severity Levels

## The Reality of Production Outages

When an alert triggers or a customer reports a problem, the first and most critical question is: *How bad is this?* In production environments, impact is rarely binary. A single endpoint timing out on a non-critical internal dashboard is vastly different from the checkout flow returning 500s for all users on Black Friday. The problem is consistently quantifying this impact under immense pressure.

## Where Teams Go Wrong

Most organizations operate with subjective, emotionally driven severity levels. If a VP notices a typo on the homepage, it suddenly becomes a "SEV1". Conversely, a silent failure in a background job that isn't processing refunds might be ignored for days because no one is screaming about it. Teams fail because their severity matrix is based on technical symptoms (e.g., "The database is down") rather than business impact.

## The Cost of Ad-Hoc Heroics

When severity is misaligned, the consequences are immediate and detrimental.

* **Alert Fatigue and Burnout:** If everything is treated as a critical emergency, engineers stop taking real emergencies seriously. Being paged at 3:00 AM for a SEV1 that turns out to be a minor log-parsing error destroys morale.
* **Wasted Resources:** Calling an all-hands-on-deck response for a minor issue pulls people away from feature work and degrades velocity.
* **Missed SLAs:** Conversely, under-classifying an incident means the right people aren't engaged quickly enough, leading to breached Service Level Agreements (SLAs) and loss of customer trust.

## An Operationally Sound Approach

Severity levels must be objective, deterministic, and strictly tied to customer or business impact. The language used must remove interpretation.

* **SEV1 (Critical):** Core business flow is completely broken for a significant percentage of users. No workaround exists. Revenue or reputation is actively burning. (e.g., "Checkout is failing for >10% of users"). Requires immediate, 24/7 all-hands response.
* **SEV2 (High):** Significant degradation of a core feature, but a workaround exists, or only a small subset of users is affected. (e.g., "Password resets are delayed by 30 minutes"). Requires immediate response during business hours, paging primary on-call off-hours.
* **SEV3 (Medium):** Minor feature is broken or internal tooling is degraded. No immediate customer impact. (e.g., "Internal analytics dashboard is stale"). Addressed during normal business hours via ticket.
* **SEV4 (Low):** Minor bugs, typos, or cosmetic issues. Backlog item.

## Decision-Making Under Pressure

The decision of what severity to assign must happen in the first 5 minutes of an incident. It should not require a debate. If there is ambiguity, the standard operational procedure is to *escalate the severity initially, and downgrade later once the impact is clarified*.

Do not base severity on the difficulty of the fix. A single missing comma that breaks the entire site is a SEV1. A complex database corruption that only affects a deprecated feature no one uses is a SEV3. Severity is about the pain the customer feels, not the pain the engineer feels fixing it.
