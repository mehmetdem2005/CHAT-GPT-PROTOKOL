# PL-006 — Security Extended Spec v1

## Purpose
PL-006 security family için business rationale, scope, actors, metrics ve decision logic ayrıntısını sağlamak.

## Business Rationale
Security failures tüm sistemi etkileyebilir. Auth, secret handling ve input controls yalnız teknik tercih değil işletim zorunluluğudur.

## Scope
- auth and session surfaces
- admin and privileged actions
- preview and runtime config exposure
- external integrations
- secrets and tokens

## Non-Scope
- generic product quality issues not affecting trust boundaries
- stylistic code issues with no security consequence

## Actors
- policy owner: security owner
- reviewers: auth owner, platform owner
- approver for temporary exception: security approver

## Decision Classes
- weak evidence but possible risk -> require_review
- confirmed secret leak path -> hard_block
- missing review on critical auth surface -> release_hold
- repeated unsafe input handling -> escalated review

## Detection Modes
- static scans
- secret exposure checks
- auth review
- policy engine mapping
- manual incident review

## Default Timelines
- critical finding immediate same-window escalation
- high finding same release cycle remediation or hold
- medium finding documented next fix window

## Metrics
- critical unresolved findings count
- secret exposure incidents count
- auth review bypass count
- mean remediation time by severity

## Evidence
- scan refs
- auth review refs
- audit logs
- deployment refs
- incident refs

## Example Scenarios
1. Secret appears in preview logs -> immediate critical handling
2. Session expiration rule removed with no review -> release hold
3. New external integration without boundary review -> require approval path

## Exception Rules
- no open-ended exception
- every exception carries expiry and mitigation
- repeat exception on same surface requires root cause review
