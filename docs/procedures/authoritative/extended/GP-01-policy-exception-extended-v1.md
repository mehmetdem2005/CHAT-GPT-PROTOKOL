# GP-01 — Policy Exception Extended Spec v1

## Purpose
Policy exception prosedürünü operasyonel ayrıntılarla genişletmek.

## Roles
- requester
- policy owner
- reviewing owner
- approving owner
- audit recorder

## Eligibility
- requester must own or operate the affected surface
- exception cannot be opened without policy reference and scope

## Required Inputs
- policyRef
- business rationale
- risk summary
- affected scope
- proposed expiry
- mitigation notes
- evidence refs

## Decision Tree
1. If policyRef missing -> reject as incomplete.
2. If affected scope undefined -> reject as incomplete.
3. If risk is critical and no mitigation exists -> escalate for approval or deny.
4. If repeat exception on same scope exceeds threshold -> require root cause review.
5. If approved -> set expiry and follow-up review.

## Default Timelines
- incomplete request should be returned in next review window
- approved exception must carry expiry
- expired exception without renewal becomes invalid by default

## Abuse Handling
- repeated unsupported exception requests may trigger governance review
- expired but still relied-on exception becomes a visible control failure

## Evidence and Records
- exception request record
- approval ref
- expiry date
- mitigation record
- follow-up review ref

## Example
Temporary exception for a non-blocking release quality rule may be accepted if mitigation and expiry are documented. Exception for confirmed tenant isolation failure should not be silently accepted.
