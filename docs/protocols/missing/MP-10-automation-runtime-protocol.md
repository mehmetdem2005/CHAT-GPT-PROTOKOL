# MP-10 — Automation Runtime Protocol

## Purpose
Automation builder çıktılarının runtime davranışını, trigger-action yürütmesini ve güvenli çalışma kurallarını taşımak.

## Producers
- A38

## Consumers
- A40
- A46
- A47

## Required Fields
- automationRuntimeId
- workflowRefs
- triggerModel
- actionModel
- failureHandling
- safetyMode
- traceId

## Optional Fields
- dryRunSupport
- auditRefs
- timeoutRules

## Validation Rules
- workflowRefs boş olamaz
- failureHandling tanımlı olmalı
- safetyMode desteklenen değerlerden biri olmalı

## Error Modes
- invalid_workflow_ref
- unsafe_action_path
- missing_failure_handling
