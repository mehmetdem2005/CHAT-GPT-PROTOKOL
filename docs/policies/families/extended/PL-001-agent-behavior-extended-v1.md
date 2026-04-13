# PL-001 — Agent Behavior Extended Spec v1

## Purpose
PL-001 family dosyasını operasyonel ve denetlenebilir ayrıntılarla genişletmek.

## Business Rationale
Ajan davranışı sistemin çekirdeğidir. Contract-first sınırlar ihlal edildiğinde yalnız tek bir output bozulmaz; preview, governance, rollback ve release kararları da tutarsızlaşır.

## Scope
- agent task execution
- patch production
- decision generation
- regeneration paths
- lock-sensitive behavior

## Non-Scope
- generic human operator errors outside agent execution
- purely static documentation edits with no agent effect

## Actors
- policy owner: platform governance lead
- primary reviewers: orchestrator owner, policy engine owner
- approver for exceptions: governance approver

## Violation Classes
- hidden dependency assumption
- silent lock overwrite
- unexplained artifact mutation
- task output without required refs
- unsafe regeneration beyond allowed scope

## Detection Modes
- automated policy engine checks
- manifest and patch validation
- manual review escalation
- release gate evidence review

## Decision Logic
- low confidence minor ambiguity -> warn
- repeated hidden dependency -> require_review
- lock overwrite attempt -> turn_block
- critical unexplained cross-scope mutation -> hard escalation path

## Default Timelines
- warn class findings reviewed in next working review window
- blocking findings require same-turn review or explicit defer decision

## Metrics
- monthly silent overwrite attempts
- unexplained patch count
- cross-scope mutation findings
- mean review resolution time for PL-001 findings

## Evidence
- task refs
- patch refs
- manifest diffs
- decision refs
- audit refs

## Example Scenarios
1. Agent modifies locked navigation choice without explicit override -> violation
2. Agent produces patch affecting unrelated admin route with no rationale -> violation
3. Agent requests review before broad regeneration -> acceptable behavior

## Exception Rules
- PL-001 exceptions are temporary only
- exception must carry owner, expiry, affected scope and mitigation note
- repeated exception on same agent path requires deeper remediation review
