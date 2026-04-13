# System Module Registry v1

Bu belge, sistemdeki ana modül sınıflarını ve rollerini görünür kılar.

## Module Classes
- studio-web
- studio-api
- orchestration-core
- policy-engine
- preview-runtime-manager
- build-worker
- manifest-store
- turn-state-store
- approval-governance
- audit-observability
- auth-and-access
- protocol-sdk
- shared-types
- agent-packages

## Required Registry Fields
- moduleId
- moduleName
- moduleClass
- ownerType
- primaryResponsibilities
- publicContracts
- dependsOnModules
- criticality

## Criticality Bands
- low
- medium
- high
- critical

## Registry Rule
Her modül public contract, sorumluluk sınırı ve ownerType alanlarıyla görünür olmalıdır.
