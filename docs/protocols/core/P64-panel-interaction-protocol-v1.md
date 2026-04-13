# P64 — Panel Interaction Protocol v1

## Purpose
Studio panel aksiyonlarını, actor rolünü ve etkilenen yüzeyleri standartlaştırmak.

## Producers
- Studio UI
- operator surfaces

## Consumers
- orchestration core
- preview sync layer
- governance handlers

## Required Fields
- protocolVersion
- panelInteractionId
- actionType
- initiatedBy
- targetSurface
- result
- traceId
- turnId

## Optional Fields
- linkedRefs
- selectedRoute
- selectedViewport
- notes

## Validation Rules
- actionType desteklenen sınıftan olmalı
- initiatedBy actor ref taşımalı
- result normalize outcome değerine uymalı
- targetSurface tanımlı yüzeylerden biri olmalı

## Example Shape
{
  "panelInteractionId": "pi_001",
  "actionType": "switch_viewport",
  "initiatedBy": {},
  "targetSurface": "preview_panel",
  "result": "applied"
}

## Error Modes
- invalid_action_type
- missing_actor_ref
- unsupported_target_surface
- invalid_result_state
