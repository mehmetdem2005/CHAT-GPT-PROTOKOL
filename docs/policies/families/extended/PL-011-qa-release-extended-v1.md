# PL-011 — QA & Release Extended Spec v1

## Purpose
PL-011 family dosyasını release-quality kararlarında yorum boşluğunu azaltacak ayrıntı düzeyine çıkarmak.

## Business Rationale
QA ve release kapıları yalnız kalite kontrol mekanizması değil, sistemin kullanıcıya ve operasyona güvenle açılmasını sağlayan karar katmanıdır. Eksik veya yüzeysel QA gate’leri, biriken kusurların release anında görünmezleşmesine ve riskin sessizce kullanıcıya aktarılmasına neden olur.

## Scope
- release candidates
- preview-backed deliverables
- QA bundle evaluation
- waivers and exceptions affecting release
- freeze and hold decisions tied to quality state
- contract-affecting change sets

## Non-Scope
- informal prototype artifacts with no release intent
- local-only experiments not connected to shared environments
- purely editorial documentation changes with no runtime effect

## Primary Actors
- family owner: release owner
- co-owner for QA integrity: quality lead or designated QA owner
- required reviewer: preview/runtime owner when preview evidence exists
- required reviewer for critical auth/privacy/security surfaces: security owner and privacy owner where applicable
- approver for final release path: release approver
- recorder: governance or release audit recorder

## Core Principles
1. No preview, no release.
2. No invisible blocker.
3. Evidence over intuition.
4. A release decision is not the same as a deployment action.
5. Deferred issues must have owners, dates and scope.

## Required Inputs
- releaseCandidateRef
- previewEvidenceRefs
- qaReportRefs
- policyDecisionRefs
- riskSummaryRef
- contractTestRefs when applicable
- waiverRefs if any
- affectedSurfaceSummary
- rollbackReadinessRef for release-affecting changes

## Gate Model
### Gate 1 — Evidence Completeness
A candidate cannot be considered release-ready unless preview evidence, required QA classes, risk summary and known waivers are all visible.

### Gate 2 — Blocking Findings Review
A candidate must be checked for unresolved critical QA findings, unresolved critical policy decisions, unresolved contract-breaking risk and preview failure without accepted mitigation.

### Gate 3 — Authorization Readiness
Before final allow, required reviewers must complete their path, waivers must carry owner and expiry, rollback or mitigation path must be visible, and a release decision record must be created.

## Blocking Taxonomy
### Category A — Immediate Release Stop
- confirmed critical security issue
- confirmed tenant isolation failure
- confirmed privacy blocker on affected scope
- preview unavailable for required release surface
- missing or invalid rollback path for high-risk release

### Category B — Release Hold Until Resolved
- missing QA bundle for critical surface
- unresolved accessibility blocker on core route
- unresolved contract validation failure
- repeated preview degradation with no accepted mitigation

### Category C — Defer With Follow-up
- non-critical performance regression with monitored mitigation
- low-severity responsive issues off the critical path
- incomplete but non-blocking documentation if tracked and owner-assigned

## Waiver Rules
A waiver is valid only if it includes blocker ref, mitigation, owner, expiry and release decision linkage. Open-ended waiver or vague justification is invalid.

## Default Timelines
- critical release blockers must be addressed within the active release window or the candidate is deferred
- missing evidence should be surfaced in the same review window
- waivers must be reviewed again before or at expiry
- deferred release decisions must carry explicit next review timing

## Detection Modes
- release review procedure
- release approval procedure
- preview diagnostics
- QA bundle evaluation
- policy decision review
- contract validation reports
- incident-triggered freeze path

## Required Records
- release decision record
- QA bundle refs
- preview refs
- blocking findings summary
- waiver refs where applicable
- rollback readiness note
- approver refs
- audit record for final decision

## Metrics
- release_hold count by reason
- releases allowed with waiver
- critical blocker escape count
- mean release decision latency
- rollback-after-release rate
- preview-missing release attempts
- unresolved QA findings older than one release cycle

## Example Scenarios
### Scenario 1 — Clean Allow
A dashboard release has full preview evidence, passing QA bundle, no critical blockers and rollback readiness documented. Outcome: allow.

### Scenario 2 — Defer
A release has acceptable preview output but missing contract validation for a changed API surface. Outcome: defer until evidence exists.

### Scenario 3 — Hold
An accessibility blocker prevents core form completion on mobile. Outcome: release_hold until blocker is fixed or re-scoped with accepted governance path.

### Scenario 4 — Hard Block
A critical tenant isolation issue is confirmed on a user-facing route. Outcome: hard_block.

## Roles and Responsibilities
### Release Owner
- ensures candidate completeness
- ensures decision record is opened
- ensures defer and hold outcomes are visible

### QA Owner
- validates bundle completeness
- classifies unresolved findings
- recommends blocking thresholds

### Security / Privacy / Specialized Reviewers
- evaluate domain-specific blockers
- confirm whether waiver path is eligible

### Release Approver
- authorizes final allow, defer or block decision
- does not erase missing evidence by assumption

## Exception Rules
- no silent exception
- no indefinite waiver
- repeated waiver on same release pattern triggers process remediation review
- confirmed critical domain blockers require explicit escalation if any override path is attempted

## Review Cadence
- every release candidate
- every major release train retrospective
- quarterly calibration of blocker taxonomy and metrics
