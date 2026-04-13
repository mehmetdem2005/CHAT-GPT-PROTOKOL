# PL-013 — Human Intervention & Governance Extended Spec v1

## Purpose
PL-013 family dosyasını lock, override, approval ve rollback kararlarında operasyonel tutarlılık sağlayacak ayrıntılarla genişletmek.

## Business Rationale
Human-in-the-loop mekanizması yalnız bir güvenlik ağı değil, sistemin geri alınabilir ve açıklanabilir kalmasının temelidir. Sessiz override veya görünmez lock değişikliği tüm governance modelini anlamsızlaştırır.

## Scope
- user locks
- operator interventions
- override actions
- approval-gated actions
- rollback suggestions and governed execution
- visible change summary obligations

## Non-Scope
- purely informational user hints with no state effect
- local throwaway experimentation with no shared state change

## Primary Actors
- family owner: platform governance lead
- reviewer: release owner when release state is affected
- reviewer: security owner when auth/privacy/tenant surface is affected
- approver: governance approver for major override paths
- recorder: audit recorder

## Governance Principles
1. User-visible locked choices are first-class control boundaries.
2. Override without rationale is prohibited.
3. Major structural changes require visible authority and evidence.
4. Rollback is a governed recovery action, not an invisible edit.
5. A change summary is part of the control surface, not cosmetic metadata.

## Required Inputs
- affected decision or artifact refs
- intervention or approval refs
- actor role and authority class
- reason summary
- impact scope
- evidence refs
- rollback option refs when applicable

## Control Types
### Lock Controls
- user_lock
- operator_lock
- policy_lock
- approval_lock
- release_lock

### Intervention Controls
- lock choice
- unlock choice
- override decision
- reroute task
- halt generation
- request regeneration
- reject output

### Recovery Controls
- suggest rollback
- execute approved rollback
- partial rollback
- release-scope rollback

## Decision Logic
### require_user_choice
- user-locked choice would otherwise be mutated
- visible user-facing structure changes need confirmation

### require_review
- operator wants to reroute or override a non-trivial path
- conflicting evidence exists around impact scope

### require_approval
- structural override crosses previously accepted boundaries
- rollback touches critical release, auth, data or tenant surfaces
- unlock affects user-locked architecture or navigation choice

### turn_block
- silent lock bypass attempted
- override lacks reason or authority
- rollback path claimed but no governed target exists

## Detection Modes
- intervention event review
- approval review
- rollback validation
- policy engine checks on lock-sensitive paths
- release review when prior user decisions are impacted

## Default Timelines
- lock-sensitive override requests must be visible in the active turn or review window
- approval-bound interventions cannot remain implied; they need recorded disposition
- rollback suggestions must convert to explicit action or explicit defer decision

## Required Records
- intervention record
- actor role record
- approval ref when required
- impacted subject refs
- rollback target refs when applicable
- user-visible summary record
- audit ref

## Metrics
- silent override attempt count
- lock-related blocking decisions count
- rollback requests by scope
- interventions resolved without complete evidence
- average time from intervention request to disposition

## Violation Examples
### Example 1
An agent changes a locked navigation model with no user or approver acknowledgment. Result: turn_block.

### Example 2
An operator requests reroute of a low-risk task and records reason, actor role and affected scope. Result: require_review, then proceed if accepted.

### Example 3
A rollback touches release-critical auth behavior without approval. Result: cannot proceed.

## Exception Rules
- no silent override exception
- temporary exception must carry owner, expiry and mitigation
- repeated use of emergency override on same pattern triggers process remediation review
- user-locked architectural choices cannot be casually reopened without visible governance path

## Relationship to Procedures
- policy exception procedure
- approval request and resolution procedures
- rollback execution and validation procedures
- release review and freeze procedures

## Review Cadence
- every major override path change
- every rollback mechanism revision
- quarterly governance control calibration review
