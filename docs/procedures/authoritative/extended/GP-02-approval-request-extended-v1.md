# GP-02 — Approval Request Extended Spec v1

## Purpose
Approval request prosedürünü role, evidence, decision completeness ve timeout davranışı açısından ayrıntılı hale getirmek.

## Roles
- requester
- subject owner
- required approver set
- governance recorder

## Eligibility
- requester must control or be responsible for affected scope
- approval subject must be concrete, not vague
- evidence refs must exist before submission unless explicit incomplete-draft path is used

## Required Inputs
- subjectRef
- scope summary
- why approval is needed
- evidenceRefs
- requested decision type
- requester identity
- due context if time-sensitive

## Decision Tree
1. If subjectRef missing -> reject as incomplete.
2. If evidence missing and no draft path allowed -> reject as incomplete.
3. If required approvers cannot be resolved -> hold for governance clarification.
4. If request is time-sensitive and high impact -> mark escalated review path.
5. If accepted -> publish pending approval record and notify approvers.

## Default Timelines
- incomplete requests should be returned in the active review window
- pending requests must show explicit owner and requested by timestamp
- stale pending approvals require visibility, not silent aging

## Required Records
- approval request record
- subject summary
- evidence bundle ref
- approver list resolution
- pending status record

## Example
A release approval request with preview refs, QA bundle and rollback readiness is complete. A request that says only "please approve release" with no linked evidence is incomplete.

## Completion
- pending
- rejected_as_incomplete
- escalated_pending
