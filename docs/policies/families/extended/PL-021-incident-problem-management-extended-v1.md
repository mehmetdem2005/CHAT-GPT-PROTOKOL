# PL-021 — Incident & Problem Management Extended Spec v1

## Purpose
PL-021 family dosyasını severity, escalation, communications, postmortem ve RCA kapanış mantığı açısından ayrıntılı hale getirmek.

## Business Rationale
Poor incident discipline causes repeated failures, invisible customer harm and governance blind spots.

## Scope
- operational incidents
- repeated systemic problems
- severity assignment
- containment and communications paths
- postmortem and RCA closure
- incident-linked release freezes

## Non-Scope
- minor local-only interruptions with no shared effect and no trend value
- generic bug tracking with no operational impact signal

## Primary Actors
- family owner: platform governance lead
- co-owner for operational handling: preview or runtime owner depending on surface
- communications owner for user-visible impact
- security or privacy owner for sensitive incident classes
- review approver for closure where needed

## Severity Model Expectations
### P1 / Critical
Broad or severe user impact, trust or control boundary concern, or active inability to operate safely.

### P2 / High
Significant degradation or repeated high-value function impairment.

### P3 / Moderate
Contained or limited operational impairment requiring tracked handling.

### P4 / Low
Minor operational event with learning value but limited impact.

## Required Inputs
- incident or event record
- initial severity assignment
- affected scope summary
- containment status
- owner assignment
- communications decision
- evidence refs

## Decision Logic
### open_and_escalate
- severity high or critical
- scope unknown but plausibly severe
- auth, privacy, tenant or release safety may be impacted

### open_and_contain
- scope is limited but real
- workaround or mitigation exists
- trend or recurrence still needs tracking

### track_as_problem
- repeated issue pattern exists even when individual events seem moderate

### cannot_close
- no timeline
- no owner
- no resolution reason
- no RCA follow-up where required

## Communications Rules
- user-visible impact requires explicit communication decision
- no-communication decisions must still carry rationale
- internal owners must not rely on implicit awareness for P1/P2 classes

## Postmortem Expectations
A postmortem should include timeline, root cause class, contributing factors, corrective actions, owners and target dates.

## RCA Closure Rules
An RCA can close only if action items have dispositions, evidence exists for remediation or mitigation, and remaining risk is recorded.

## Detection Modes
- operational event declaration
- runtime health review
- release freeze or rollback triggers
- auth, privacy or vendor review procedures
- repeated trend review across event records

## Default Timelines
- high-severity incidents require immediate same-window visibility
- closure should not happen before ownership and follow-up are assigned
- repeated incidents should be grouped into problem review without waiting for manual memory

## Required Records
- incident or event record
- severity assignment record
- communications decision note
- postmortem ref where required
- RCA closure ref where applicable
- audit or review refs

## Metrics
- incident count by severity
- repeated issue count
- mean time to assign owner
- mean time to containment
- mean time to closure
- postmortem completion rate for required classes

## Example Scenarios
### Scenario 1
A preview runtime outage affects broad user-facing validation during release review. Result: operational incident with possible freeze.

### Scenario 2
A repeated vendor timeout causes frequent but contained degradation across two release cycles. Result: problem management path.

### Scenario 3
A high-severity auth-related event resolves quickly but lacks postmortem and communication rationale. Result: closure incomplete.

## Exception Rules
- no silent closure for required postmortem classes
- no severity downgrade without rationale
- repeated incidents with same pattern cannot be treated as unrelated noise indefinitely

## Relationship to Procedures
- operational event declaration procedure
- postmortem procedure
- RCA closure procedure
- release freeze procedure
- auth incident response procedure
- performance degradation response procedure

## Review Cadence
- every high-severity incident
- every quarterly problem trend review
- after major incident process failures
