# Proposed New Protocols v1

Bu belge, mevcut Protocol Registry v1 taramasından sonra eksik görülen yeni protokol adaylarını tanımlar.

## Amaç
- Registry’de numarası boş veya kapsamı eksik kalan alanları doldurmak
- Uygulama, preview, QA, governance ve protocol lifecycle boşluklarını kapatmak
- Gelecekteki `Protocol Registry v2` için aday çekirdek liste üretmek

---

# 1. Önerilen Yeni Protokoller

## P08 — Request Context Protocol
**Neden gerekli:**
Core envelope alanları dağınık; request bazlı kimlik, actor, workspace, session, turn ve trace bağlamı tek protokol altında net değil.

**Amaç:**
Tüm request tabanlı akışlarda kullanılan standart context taşıyıcısı olmak.

**Önerilen alanlar:**
- requestId
- actor
- workspaceId
- sessionId
- turnId
- traceId
- sourceSurface
- authContextRef

---

## P09 — Capability Declaration Protocol
**Neden gerekli:**
Ajanlar ve servisler neyi yapabildiğini resmi olarak beyan etmiyor. Orchestrator ve governance için capability görünürlüğü eksik.

**Amaç:**
Ajan veya servis yeteneklerini, kabul ettiği input tiplerini ve ürettiği output tiplerini ilan etmek.

**Önerilen alanlar:**
- capabilityId
- ownerId
- supportedTaskTypes
- acceptedInputProtocols
- emittedOutputProtocols
- limitations
- version

---

## P18 — Decision Confidence Protocol
**Neden gerekli:**
Karar confidence sinyalleri farklı protokollerde dağınık ve standart değil.

**Amaç:**
Karar veya öneri güven skorunu, evidence ve uncertainty ile birlikte taşımak.

**Alanlar:**
- confidenceId
- decisionRef
- confidenceScore
- uncertaintyNotes
- evidenceRefs

---

## P19 — Requirement Completeness Protocol
**Neden gerekli:**
Requirements capture sonrası ne kadar eksik bilgi kaldığı resmi değil.

**Amaç:**
Bir requirement setinin tamlık seviyesini ve kalan kritik boşlukları tanımlamak.

**Alanlar:**
- completenessId
- requirementRef
- completenessScore
- blockingUnknowns
- recommendedClarifications

---

## P39 — Design Review Summary Protocol
**Neden gerekli:**
Variation ve visual outputs var ama tasarım review özetinin ortak taşıyıcısı eksik.

**Amaç:**
Görsel seçenekler, art direction, token ve preview sonuçlarını tek review özetinde birleştirmek.

**Alanlar:**
- reviewSummaryId
- candidateRefs
- selectedCandidateRef
- rejectedCandidateRefs
- rationale
- previewEvidenceRefs

---

## P53 — Module Boundary Protocol
**Neden gerekli:**
Modüllerin neyi dışa açtığı ve neyi içte tuttuğu resmi değil.

**Amaç:**
Modül sınırlarını, public/private artifact’ları ve allowed dependency yönlerini tanımlamak.

**Alanlar:**
- moduleId
- publicArtifacts
- internalArtifacts
- allowedImports
- forbiddenDependencies

---

## P54 — Repository Topology Protocol
**Neden gerekli:**
Monorepo içinde klasör, package ve ownership ilişkisi için ayrı protokol yok.

**Amaç:**
Repo klasör ağacını, package rollerini ve ownership kurallarını sözleşme haline getirmek.

**Alanlar:**
- topologyId
- packageMap
- appMap
- agentMap
- ownershipMap
- dependencyZones

---

## P55 — Patch Validation Protocol
**Neden gerekli:**
Code patch var ama patch’in doğrulandığına dair ortak sonuç protokolü yok.

**Amaç:**
Bir patch’in syntax, type, contract, QA ve policy doğrulama sonuçlarını taşımak.

**Alanlar:**
- patchValidationId
- patchRef
- syntaxStatus
- typeStatus
- contractStatus
- qaRefs
- policyRefs

---

## P56 — Code Generation Provenance Protocol
**Neden gerekli:**
Hangi ajan hangi artifact’ı hangi girdilerle üretti bilgisi dağınık.

**Amaç:**
Kod üretim provenansını resmi hale getirmek.

**Alanlar:**
- provenanceId
- artifactRef
- producedByAgentId
- sourceInputRefs
- sourceDecisionRefs
- sourceTaskRef
- generatedAt

---

## P57 — Dependency Risk Protocol
**Neden gerekli:**
External dependency bilgisi var ama risk skoru ve approval mantığı tek protokol değil.

**Amaç:**
Bağımlılık riskini, SLA yeterliliğini ve fallback varlığını taşımak.

**Alanlar:**
- dependencyRiskId
- dependencyRef
- riskLevel
- slaAdequacy
- approvalRequired
- fallbackAvailable

---

## P58 — Feature Flag Protocol
**Neden gerekli:**
Deployment ve release belgelerinde feature flag yönetimi var ama protokol yok.

**Amaç:**
Feature flag tanımı, sahibi, rollout scope’u ve cleanup zorunluluğunu taşımak.

**Alanlar:**
- flagId
- ownerRef
- environments
- rolloutScope
- expiryDate
- cleanupRequired

---

## P59 — Configuration Surface Protocol
**Neden gerekli:**
Config değişiklikleri ve environment ayrımları için bağımsız sözleşme eksik.

**Amaç:**
Ayarlanabilir config yüzeylerini, scope ve risk derecelerini tanımlamak.

**Alanlar:**
- configSurfaceId
- configKeys
- environments
- sensitivityBand
- mutableAtRuntime
- approvalRequired

---

## P65 — Route Validation Protocol
**Neden gerekli:**
Preview Runtime belgesinde route validation var ama registry’de ayrı protokol yok.

**Amaç:**
Route bazlı validation sonuçlarını standartlaştırmak.

**Alanlar:**
- validationId
- previewSessionId
- routeRef
- renderStatus
- navigationReachable
- directLoadSuccess
- httpStatus

---

## P66 — Preview Diagnostic Protocol
**Neden gerekli:**
Preview Diagnostics Taxonomy mevcut ama registry’de protokol taşıyıcısı eksik.

**Amaç:**
Preview diagnostic item’larını ortak yapı ile taşımak.

**Alanlar:**
- diagnosticId
- diagnosticCode
- diagnosticDomain
- severity
- routeRef
- viewportId
- releaseImpact
- recoveryClass

---

## P67 — Viewport Profile Protocol
**Neden gerekli:**
Viewport id’leri kullanılıyor ama profil tanımı protokolleşmemiş.

**Amaç:**
Desktop/tablet/mobile ve özel viewport setlerini tanımlamak.

**Alanlar:**
- viewportId
- width
- height
- interactionMode
- deviceClass
- orientation

---

## P68 — Build Artifact Protocol
**Neden gerekli:**
Build sonucunda çıkan artifact’ların standardı eksik.

**Amaç:**
Build çıktılarını, bundle ref’lerini ve retention metadata’sını tanımlamak.

**Alanlar:**
- buildArtifactId
- buildRef
- artifactRefs
- outputType
- storageRef
- retentionClass

---

## P69 — Runtime Health Protocol
**Neden gerekli:**
Runtime health sinyalleri ayrı protokol olarak standart değil.

**Amaç:**
Runtime health/readiness sonuçlarını standartlaştırmak.

**Alanlar:**
- runtimeHealthId
- runtimeId
- liveness
- readiness
- failedChecks
- observedAt

---

## P78 — Release Readiness QA Protocol
**Neden gerekli:**
QA report’lar var ama release readiness birleşik sonucu yok.

**Amaç:**
QA bulgularının release’e etkisini tek sonuç paketine toplamak.

**Alanlar:**
- readinessQaId
- qaReportRefs
- releaseBlockingIssues
- warnings
- recommendation

---

## P79 — Test Evidence Bundle Protocol
**Neden gerekli:**
Farklı test raporlarını release/gov kararları için toplu taşımak zor.

**Amaç:**
Test kanıt paketini, report refs ve summaries ile taşımak.

**Alanlar:**
- evidenceBundleId
- reportRefs
- summary
- blockingFindings
- relatedArtifactRefs

---

## P92 — Incident Record Protocol
**Neden gerekli:**
Incident runbook var ama incident taşıyıcı protokol registry’de yok.

**Amaç:**
Incident kayıtlarını, severity ve lifecycle ile standartlaştırmak.

**Alanlar:**
- incidentId
- severity
- title
- affectedEnvironments
- affectedRefs
- currentStatus
- containmentActions

---

## P93 — Problem Record Protocol
**Neden gerekli:**
Tekrarlayan incident’leri problem management altında toplamak için protokol eksik.

**Amaç:**
Problem kayıtlarını ve bağlı incident’leri taşımak.

**Alanlar:**
- problemId
- title
- rootCauseClass
- linkedIncidentRefs
- openActions
- ownerRef

---

## P94 — Rollout Strategy Protocol
**Neden gerekli:**
Canary, rolling, blue-green kararları deployment belgesinde var ama protokol yok.

**Amaç:**
Bir release için rollout stratejisini açıkça tanımlamak.

**Alanlar:**
- rolloutId
- releaseRef
- strategyType
- trafficPlan
- successMetrics
- rollbackTriggerRules

---

## P95 — Backup Restore Validation Protocol
**Neden gerekli:**
Restore readiness için policy ve incident belgeleri var ama teknik taşıyıcı protokol yok.

**Amaç:**
Backup/restore validation sonuçlarını standartlaştırmak.

**Alanlar:**
- restoreValidationId
- backupRef
- restoreTargetRef
- validationChecks
- outcome
- observedAt

---

## P96 — Secret Exposure Response Protocol
**Neden gerekli:**
Secret exposure riskleri error/policy düzeyinde var ama response plan protokolü yok.

**Amaç:**
Secret exposure tespit edildiğinde containment ve rotation akışını standartlaştırmak.

**Alanlar:**
- responseId
- secretClass
- affectedSurfaces
- containmentActions
- rotationRequired
- resolutionStatus

---

## P97 — Tenant Isolation Evidence Protocol
**Neden gerekli:**
Multi-tenancy policy güçlü ama isolation evidence taşıyıcısı eksik.

**Amaç:**
Tenant isolation kontrollerinin teknik kanıtını taşımak.

**Alanlar:**
- evidenceId
- tenantScope
- checkedLayers
- findings
- blocking
- evidenceRefs

---

## P98 — Change Request Protocol
**Neden gerekli:**
Change/config management için resmi request nesnesi yok.

**Amaç:**
Schema, config, protocol veya topology değişiklik isteklerini standartlaştırmak.

**Alanlar:**
- changeRequestId
- changeType
- impactSummary
- approvalRefs
- rollbackPlanRef
- targetRefs

---

## P99 — Protocol Deprecation Notice Protocol
**Neden gerekli:**
Protocol lifecycle governance için deprecation bildirimi taşıyıcısı eksik.

**Amaç:**
Deprecated protokol, alan veya davranışları resmi biçimde ilan etmek.

**Alanlar:**
- deprecationId
- protocolRef
- deprecatedFields
- replacementRef
- sunsetVersion
- migrationNotes

---

# 2. Öncelikli Yeni Protokol Seti

İlk eklenmesi en değerli görünenler:
1. P08 Request Context Protocol
2. P09 Capability Declaration Protocol
3. P55 Patch Validation Protocol
4. P65 Route Validation Protocol
5. P66 Preview Diagnostic Protocol
6. P69 Runtime Health Protocol
7. P78 Release Readiness QA Protocol
8. P92 Incident Record Protocol
9. P94 Rollout Strategy Protocol
10. P98 Change Request Protocol
11. P99 Protocol Deprecation Notice Protocol

---

# 3. Registry v2 İçin Öneri

Bir sonraki registry sürümünde şu yapı önerilir:
- mevcut P01–P91 korunur
- yeni P08, P09 ve diğer boş numaralar doldurulur
- P64, P70–P79 ve P80–P99 arası genişletilir
- her protokol için minimum alan seti + error modes + lifecycle + fixture zorunluluğu eklenir

---

# 4. Sonuç
Mevcut protokol omurgası güçlüdür; ancak uygulama, preview, release, incident ve change governance taraflarında yeni protokol adayları eklenirse sistem daha az yorum boşluğu ile geliştirilebilir hale gelir.
