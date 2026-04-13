# MP-09 — Admin Module Protocol

## Purpose
Admin modülünün ekran grupları, erişim yüzeyleri ve artifact kapsamını tanımlamak.

## Producers
- A37

## Consumers
- A41
- A47
- A49

## Required Fields
- adminModuleId
- moduleSections
- permissionRefs
- routeRefs
- artifactRefs
- traceId

## Optional Fields
- bulkActionRules
- auditRequirements
- densityHints

## Validation Rules
- permissionRefs boş olamaz
- routeRefs admin surface ile uyumlu olmalı
- moduleSections en az bir section içermeli

## Error Modes
- missing_permission_refs
- invalid_admin_route
- missing_admin_artifacts
