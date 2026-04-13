# P48 — Workflow Protocol v1

## Purpose
Workflow state'leri, transitions, side effects ve compensations yapısını standartlaştırmak.

## Producers
- workflow agents
- automation agents

## Consumers
- automation runtime
- backend planning
- validation and review layers

## Required Fields
- protocolVersion
- workflowId
- states
- transitions
- sideEffects
- compensations
- traceId
- turnId

## Optional Fields
- triggerRefs
- timeoutRules
- rollbackHints
- auditRequirements

## Validation Rules
- states boş olamaz
- transitions tanımlı state refs kullanmalı
- sideEffects compensation ihtiyacı taşıyorsa işaretlenmeli
- terminal state en az bir tane bulunmalı

## Example Shape
{
  "workflowId": "wf_001",
  "states": [],
  "transitions": [],
  "compensations": [],
  "sideEffects": []
}

## Error Modes
- missing_states
- invalid_transition_ref
- missing_terminal_state
- uncompensated_side_effect
