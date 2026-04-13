# MP-07 — Visual Consistency Report Protocol

## Purpose
Görsel drift, token ihlali ve tutarsız component davranışlarını raporlamak.

## Producers
- A28

## Consumers
- A41
- A43
- A44
- A48

## Required Fields
- visualConsistencyReportId
- checkedSurfaces
- driftFindings
- severitySummary
- recommendedFixes
- traceId

## Optional Fields
- captureRefs
- tokenRefs
- componentRefs

## Validation Rules
- checkedSurfaces boş olamaz
- driftFindings en az bir surface ile ilişkilendirilmeli
- severitySummary normalize değer taşımalı

## Error Modes
- missing_surface_refs
- invalid_drift_classification
- missing_recommended_fix
