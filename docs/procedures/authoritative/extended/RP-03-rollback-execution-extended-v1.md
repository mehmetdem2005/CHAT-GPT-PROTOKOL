# RP-03 — Rollback Execution Extended Spec v1

## Purpose
Rollback execution prosedürünü target resolution, approval coupling, safety checks ve post-action record zorunluluğu ile ayrıntılı hale getirmek.

## Roles
- rollback requester
- rollback executor
- release owner when release scope is affected
- governance approver when approval-bound scope exists
- validation owner

## Required Inputs
- rollback target ref
- affected scope summary
- approval ref where needed
- latest manifest ref
- current release or turn state ref
- evidence for why rollback is chosen

## Decision Tree
1. If target ref cannot be resolved, stop and request clarification.
2. If rollback touches approval-bound scope and no approval exists, do not execute.
3. If manifest or affected scope is inconsistent, hold for review.
4. If release-critical scope is involved, notify release owner before execution.
5. After execution, trigger validation path immediately.

## Safety Checks
- target exists
- scope is explicit
- approval requirement evaluated
- expected blast radius understood
- post-rollback validation owner assigned

## Default Timelines
- rollback should not remain half-decided without explicit pending state
- post-execution validation should be scheduled immediately
- unresolved rollback ambiguity should block execution, not be guessed away

## Required Records
- rollback execution record
- target resolution note
- approval linkage
- manifest update note
- post-rollback validation trigger record
- audit ref

## Example
A rollback for a release candidate with a known safe snapshot and explicit affected routes can proceed after approval check. A rollback request that says only "go back to previous state" without target resolution cannot execute.

## Completion
- rollback_executed
- rollback_blocked_for_review
- rollback_denied_missing_approval
