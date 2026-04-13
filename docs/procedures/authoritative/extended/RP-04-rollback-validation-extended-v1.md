# RP-04 — Rollback Validation Extended Spec v1

## Purpose
Rollback validation prosedürünü artifact integrity, route availability, smoke QA ve closure decision mantığıyla ayrıntılı hale getirmek.

## Roles
- validation owner
- release owner when release scope is affected
- runtime owner when preview validation is required
- governance reviewer when rollback remains disputed

## Required Inputs
- rollback execution ref
- target snapshot ref
- affected scope summary
- latest manifest ref
- preview and route validation refs where applicable
- QA smoke refs

## Decision Tree
1. If rollback execution record missing, validation cannot start.
2. If actual artifact set differs materially from expected target scope, open review state.
3. If required route or preview validation fails, rollback is not considered fully validated.
4. If smoke QA reveals a new blocker, escalate before closure.
5. If all required checks pass, mark rollback validated.

## Validation Areas
- artifact integrity
- manifest consistency
- route availability
- preview readiness
- smoke QA status
- release gate impact

## Default Timelines
- validation should begin immediately after rollback execution
- unresolved validation cannot silently age into closure
- release-scope rollbacks should not re-enter allow state until validation is explicit

## Required Records
- validation result record
- failed check summary if any
- route and preview evidence refs
- QA smoke refs
- closure or follow-up decision record

## Example
A rollback returns the codebase to a safe snapshot but route validation still fails on a core page. Result: rollback executed but not validated.

## Completion
- rollback_validated
- rollback_invalid
- rollback_needs_followup
