# Artifact Manifest Schema v1

Bu belge, üretilen tüm dosya, klasör, yapılandırma, build çıktısı ve preview artifact’larının resmi manifest şemasını tanımlar.

## Amaç
- her artifact’ın neden var olduğunu açıklamak
- hangi ajan tarafından üretildiğini kayıt altına almak
- hangi modüle, contract’a ve politika setine bağlı olduğunu göstermek
- patch, preview, QA, audit ve rollback akışlarını dosya seviyesinde izlenebilir kılmak

## Tasarım İlkeleri
- every artifact has a reason
- every artifact has an owner
- every artifact is traceable
- every artifact is impact-aware
- every critical artifact is reversible
- manifest append-friendly olmalıdır

## Üst Düzey Bölümler
1. Manifest Identity
2. Workspace Context
3. Artifact Registry
4. Module Ownership Map
5. Dependency Graph
6. Entry Point Map
7. Contract Impact Map
8. Route and Preview Impact Map
9. QA Coverage Map
10. Snapshot and Rollback Map
11. Audit and Trace Links
12. Integrity Rules

## Manifest Identity
Zorunlu alanlar:
- manifestId
- manifestVersion
- workspaceId
- sessionId
- generatedAt
- generatedBy
- basedOnSnapshotId
- manifestScope

Manifest scope değerleri:
- workspace_full
- module_partial
- turn_delta
- release_candidate
- rollback_snapshot

## Workspace Context
Zorunlu alanlar:
- projectId
- productGoalRef
- activeStage
- activeArchitectureRef
- activeTokenPackRef
- activePolicyPackRef

## Artifact Registry
Her artifact için temel alanlar:
- artifactId
- artifactType
- logicalName
- path
- status
- moduleRef
- ownedByAgent
- primaryPurpose
- createdInTurnId
- lastModifiedInTurnId
- patchRefs
- sourceOfTruth
- criticality

Önerilen ek alanlar:
- language
- framework
- format
- tags
- humanReadableDescription
- dependsOnArtifacts
- usedByArtifacts
- exports
- imports
- entryPointRole
- previewRelevance
- qaCoverageRefs
- policyRefs
- contractRefs
- snapshotRefs
- rollbackEligible

Artifact type değerleri:
- page
- component
- layout
- route_config
- style
- design_token
- schema
- type_definition
- api_contract
- service
- database_model
- migration
- auth_config
- workflow_definition
- integration_config
- build_config
- runtime_config
- test
- qa_output
- preview_snapshot
- asset
- documentation

Status değerleri:
- planned
- generated
- modified
- validated
- blocked
- deprecated
- rolled_back
- deleted

Criticality değerleri:
- low
- medium
- high
- critical

## Module Ownership Map
Her modül kaydı:
- moduleId
- moduleName
- ownedArtifacts
- publicArtifacts
- internalArtifacts
- ownerAgents
- dependsOnModules
- usedByModules

Kurallar:
- bir artifact en az bir modüle bağlı olmalıdır
- public artifact’lar diğer modüllerce kullanılabilir
- internal artifact’lar doğrudan çapraz modül import’u için kullanılamaz

## Dependency Graph
Artifact dependency kaydı:
- fromArtifactId
- toArtifactId
- dependencyType
- direction
- critical

Dependency type değerleri:
- imports
- extends
- implements_contract
- consumes_schema
- uses_tokens
- uses_route
- calls_service
- requires_config
- loads_asset

External dependency kaydı:
- dependencyId
- name
- category
- usedByArtifacts
- riskLevel
- approvalRequired

External category değerleri:
- npm_package
- runtime_service
- database
- cdn_asset
- oauth_provider
- monitoring_provider
- payment_provider
- email_provider

## Entry Point Map
Her entry point:
- entryPointId
- entryType
- artifactRef
- routeRef
- runtimeRole
- authRequirement
- previewPriority

Entry type değerleri:
- app_root
- page_route
- api_route
- admin_route
- automation_builder
- settings_route
- background_worker
- build_entry
- preview_entry

Runtime role değerleri:
- user_facing
- admin_facing
- system_internal
- qa_internal

## Contract Impact Map
Her kayıt:
- artifactRef
- protocolRefs
- apiContractRefs
- schemaRefs
- policyRefs
- impactLevel
- breakingChangeRisk

Impact level değerleri:
- minor
- moderate
- major
- systemic

Breaking change risk değerleri:
- none
- possible
- likely
- confirmed

Kural:
- contract etkisi olan artifact’larda contract refs boş bırakılamaz
- breaking risk likely veya confirmed ise contract test ve approval gerekir

## Route and Preview Impact Map
Route impact kaydı:
- artifactRef
- affectedRoutes
- routeType
- requiresRetest
- criticalFlowImpact

Route type değerleri:
- marketing
- authenticated_app
- admin
- automation
- settings
- system

Preview impact kaydı:
- artifactRef
- desktopImpact
- tabletImpact
- mobileImpact
- expectedVisualDelta
- snapshotRefs

Kural:
- page, component, layout, style ve design_token türleri preview impact üretmelidir

## QA Coverage Map
Her coverage kaydı:
- artifactRef
- qaTypes
- reportRefs
- lastCheckedAt
- coverageStatus
- blockingFindingsCount

QA type değerleri:
- code_review
- static_analysis
- responsive_qa
- accessibility_qa
- performance_qa
- security_qa
- regression_qa
- contract_test

Coverage status değerleri:
- not_checked
- partially_checked
- checked
- blocked

## Snapshot and Rollback Map
Snapshot kaydı:
- snapshotId
- artifactRef
- snapshotType
- createdAt
- createdInTurnId
- storageRef
- approved

Snapshot type değerleri:
- initial_generation
- post_patch
- pre_release
- post_approval
- rollback_safe_point

Rollback target kaydı:
- rollbackId
- targetSnapshotId
- affectedArtifacts
- rollbackScope
- approvedBy
- createdAt

Rollback scope değerleri:
- single_artifact
- module_wide
- turn_delta
- release_candidate

## Audit and Trace Links
Her trace link:
- artifactRef
- turnRefs
- taskRefs
- decisionRefs
- auditRefs
- approvalRefs
- riskRefs

Kural:
- kritik artifact değişikliklerinde en az bir taskRef, bir turnRef ve bir auditRef bulunmalıdır

## Integrity Rules
- artifact uniqueness
- path uniqueness
- owner presence
- contract binding
- QA consistency
- rollback consistency
- audit consistency

## Artifact Yaşam Döngüsü
1. planned
2. generated
3. modified
4. validated
5. deprecated veya rolled_back veya deleted

Kurallar:
- validated statüsü için kritik QA kapsamı temiz olmalıdır
- deleted artifact geçmişten silinmez, pasif duruma alınır
- rolled_back durumunda hedef snapshot bağı zorunludur

## Minimum Çekirdek Alanlar
- manifestId
- manifestVersion
- workspaceId
- generatedAt
- generatedBy
- manifestScope
- artifacts
- artifactId
- artifactType
- path
- status
- moduleRef
- ownedByAgent
- primaryPurpose
- createdInTurnId
- lastModifiedInTurnId
- patchRefs
- criticality
- entryPoints
- contractImpacts
- qaCoverage
- traceLinks

## Sonuç
Bu belge, sistemin dosya, kod ve üretim çıktıları için resmi kayıt omurgasını tanımlar.
