# PL-014 — Deployment & Release Management Extended Spec v1

## Purpose
PL-014 family dosyasını gerçek işletim ayrıntılarıyla genişletmek ve deployment / release yüzeyinde karar boşluğunu azaltmak.

## Business Rationale
Deployment ve release hataları yalnız teknik kusur üretmez; kullanıcı etkisi, veri bütünlüğü riski, güven kaybı ve governance ihlali yaratır. Bu nedenle deployment kararı yalnız pipeline sonucu değil, evidence temelli bir işletim kararıdır.

## Scope
- production deployment requests
- release candidates
- rollout strategy decisions
- freeze and unfreeze actions
- rollback readiness checks
- hotfix release paths
- feature-flag mediated releases

## Non-Scope
- local developer experimentation
- non-shared disposable sandboxes with no user impact
- documentation-only changes that do not alter release surfaces

## Primary Actors
- family owner: release owner
- required reviewer: preview/runtime owner
- required reviewer for critical surfaces: security owner
- optional reviewer: compliance owner when regulated surface is involved
- approver for production cutover: release approver
- audit recorder: governance or pipeline recorder

## Required Inputs
- release candidate ref
- preview evidence refs
- QA bundle refs
- policy decision refs
- rollout strategy ref
- rollback readiness ref
- affected environment list
- change summary

## Decision Gates
### Gate A — Candidate Integrity
Release candidate aşağıdaki minimumları karşılamalıdır:
1. preview evidence mevcut olmalı
2. required QA bundle mevcut olmalı
3. critical policy blocker bulunmamalı
4. affected scope documented olmalı

### Gate B — Deployment Safety
1. rollout strategy seçilmiş olmalı
2. rollback path documented olmalı
3. environment-specific risks yazılmış olmalı
4. critical owner notifications hazırlanmış olmalı

### Gate C — Final Authorization
1. required approvers tamamlanmalı
2. open blocker sayısı sıfır olmalı veya explicit waiver taşımalı
3. hotfix ise fast-path justification bulunmalı

## Rollout Strategy Classes
- canary
- rolling
- blue_green
- controlled_flag_enablement
- restricted_internal_rollout

## Strategy Selection Rules
- unknown risk and user-facing change -> canary or restricted rollout preferred
- data-model coupled release -> stronger rollback evidence required
- auth or tenant surface release -> security-aware review mandatory
- hotfix with limited scope -> rolling or restricted path may be acceptable if evidence exists

## Enforcement Logic
### allow_with_review
- candidate complete
- no critical blocker
- low or moderate rollout risk

### release_hold
- missing rollback readiness
- missing evidence bundle
- unresolved critical QA or policy finding
- required approver missing

### hard_block
- deployment would bypass defined production approval path
- rollout strategy absent on critical release
- confirmed tenant/auth/privacy blocker present

## Detection Modes
- pipeline gate checks
- release checklist review
- policy engine mapping
- manual governance review
- incident-driven release freeze

## Default Timelines
- production release review should conclude within the active release window
- missing evidence should be surfaced in the same review window, not after deployment
- freeze decisions should be recorded immediately when invoked
- rollback readiness must be evaluated before final approval, not after cutover

## Required Records
- release decision record
- rollout strategy record
- rollback readiness record
- approver refs
- environment scope note
- release audit record

## Metrics
- releases blocked for missing evidence
- releases blocked for missing approver
- post-release rollback rate
- hotfix ratio per release train
- freeze invocations per quarter
- mean release decision latency

## Violation Classes
### Minor
- incomplete release summary with otherwise recoverable evidence
- outdated but still understandable rollout note

### Major
- missing required approver
- release candidate without explicit rollout strategy
- release hold ignored in manual execution path

### Critical
- production cutover without authorized path
- deployment despite unresolved critical blocker
- rollback path claimed but not actually available

## Example Scenarios
### Scenario 1 — Acceptable Canary
A user-facing dashboard release has preview evidence, QA bundle, rollback ref and canary rollout plan. One low-severity non-blocking issue remains with explicit follow-up. Result: allow with tracked follow-up.

### Scenario 2 — Release Hold
A production release includes schema-affecting changes but rollback readiness is not documented. Result: release_hold until readiness evidence exists.

### Scenario 3 — Hard Block
A critical auth surface change is attempted in production without required approval chain. Result: hard_block.

## Exception Rules
- exceptions are temporary only
- every exception requires explicit expiry and mitigation note
- repeated exception on the same release pattern triggers process remediation review
- exception cannot erase the audit trail

## Relationship to Procedures
This family is operationalized by:
- release review / approval procedures
- release freeze procedure
- hotfix procedure
- rollback execution and validation procedures

## Review Cadence
- every production release
- every hotfix path invocation
- quarterly release process review
