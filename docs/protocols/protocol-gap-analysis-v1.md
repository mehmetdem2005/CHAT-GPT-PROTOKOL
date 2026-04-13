# Protocol Gap Analysis v1

Bu belge, mevcut Protocol Registry v1 içindeki tanımlı protokollerin her biri için eksik, muğlak veya geliştirilmesi gereken alanları tek tek değerlendirir.

## Amaç
- Her protokolün uygulanabilirlik olgunluğunu artırmak
- Sadece isim düzeyinde kalan protokolleri schema-ready hale yaklaştırmak
- Protokoller arası boşlukları ve yeni protokol ihtiyaçlarını görünür kılmak

## İnceleme Ölçütleri
Her protokol şu başlıklarda değerlendirildi:
- alan yeterliliği
- lifecycle netliği
- error mode yeterliliği
- auth / audit / trace bağı
- QA / preview / release etkisi
- fixture ve validator hazırlık düzeyi

## Olgunluk Etiketleri
- `M1`: sadece isim/amaç düzeyinde
- `M2`: kısmi alan tanımı var
- `M3`: uygulanabilir ama eksikleri var
- `M4`: güçlü çekirdek, küçük açıklar var

---

# 1. Core Envelope Protocols

## P01 — Task Contract Protocol
- Olgunluk: M3
- Güçlü yan: temel required/optional alanlar var
- Eksik:
  - `idempotencyKey` yok
  - `timeoutMs` ve `retryPolicy` açık alan olarak yok
  - `inputMode` ve `outputContractRefs` ayrımı net değil
  - `taskScope` ve `sideEffectClass` eksik
- Geliştirme:
  - execution safety alanları eklenmeli
  - approval-required task’ler için `approvalBoundary` eklenmeli
  - `dependsOnTaskIds` ile `blockingDependencies` ayrıştırılmalı

## P02 — Task Graph Protocol
- Olgunluk: M3
- Eksik:
  - node ve edge şeması net değil
  - graph lifecycle yok
  - supersede edilen graph ilişkisi yok
  - `graphReason` ve `graphKind` eksik
- Geliştirme:
  - `graphStatus`, `entryNodes`, `terminalNodes`, `blockedNodes` eklenmeli
  - reroute/supersede semantiği eklenmeli

## P03 — Turn State Protocol
- Olgunluk: M4
- Güçlü yan: ayrı dokümanla destekleniyor
- Eksik:
  - state diff / delta taşıma biçimi net değil
  - snapshot reference zorunluluğu registry seviyesinde görünür değil
  - `workspaceId` ve `sessionId` registry özetinde yok
- Geliştirme:
  - `stateVersion` ve `snapshotRef` registry’ye eklenmeli
  - turn transition guard’ları registry içinde kısaca yazılmalı

## P04 — Decision Log Protocol
- Olgunluk: M3
- Eksik:
  - append-only garantisi registry’de yazılı değil
  - `confidence`, `locked`, `reversible`, `subjectType` alanları eksik
- Geliştirme:
  - decision conflict refs eklenmeli
  - `decisionCategory` zorunlu olmalı

## P05 — Decision Memory Protocol
- Olgunluk: M3
- Eksik:
  - active view ile historical snapshot ayrımı net değil
  - `lastUpdatedInTurnId` yok
  - rejection reason modeli eksik
- Geliştirme:
  - `activePreferences`, `lockedChoices`, `rejectedAlternatives`, `derivedDefaults` ayrıştırılmalı

## P06 — Event Contract Protocol
- Olgunluk: M4
- Eksik:
  - `subjectRef`, `subjectType`, `correlationRefs` yok
  - event producer capability ve event class yok
- Geliştirme:
  - `idempotencyKey` zorunluya yakın hale getirilmeli
  - replay ve ordering notları eklenmeli

## P07 — Error Envelope Protocol
- Olgunluk: M4
- Güçlü yan: hata omurgasıyla destekleniyor
- Eksik:
  - `errorFamily`, `sourceLayer`, `recoveryClass`, `escalationClass` registry özetinde yok
  - user-facing vs technical summary ayrımı yok
- Geliştirme:
  - multi-surface message refs eklenmeli
  - `status=open|resolved` benzeri lifecycle desteklenmeli

---

# 2. Discovery & Decision Protocols

## P10 — User Intent Protocol
- Olgunluk: M2
- Eksik:
  - product class candidate yapısı tanımlı değil
  - confidence alanı zorunlu mu belirsiz
  - assumption listesi yok
- Geliştirme:
  - `primaryIntent`, `productTypeCandidates`, `confidence`, `assumptions` netleşmeli

## P11 — Discovery Summary Protocol
- Olgunluk: M2
- Eksik:
  - `openQuestions`, `targetUserHints`, `coreGoal` alanları resmi değil
- Geliştirme:
  - downstream question generation için resmi minimum alan seti yazılmalı

## P12 — Requirements Capture Protocol
- Olgunluk: M2
- Eksik:
  - raw answers ile normalized capture ayrımı belirsiz
  - file upload / asset references düşünülmemiş
- Geliştirme:
  - `captureSource`, `rawValue`, `normalizedValue`, `captureConfidence` eklenmeli

## P13 — Structured Requirements Protocol
- Olgunluk: M3
- Eksik:
  - FR / NFR / constraints / unknowns ayrımı registry’de yok
  - trace to original answers eksik
- Geliştirme:
  - `functionalRequirements`, `nonFunctionalRequirements`, `constraints`, `unknowns`, `sourceAnswerRefs` netleşmeli

## P14 — Clarification Plan Protocol
- Olgunluk: M2
- Eksik:
  - clarification priority ve blocking question ayrımı yok
- Geliştirme:
  - `clarificationItems`, `blocking`, `reason`, `nextBestQuestion` alanları eklenmeli

## P15 — Feature Priority Protocol
- Olgunluk: M2
- Eksik:
  - scoring modeli yok
  - must/should/could sınıfı yok
- Geliştirme:
  - `priorityBand`, `valueScore`, `riskScore`, `phaseRecommendation` eklenmeli

## P16 — Persona Protocol
- Olgunluk: M2
- Eksik:
  - persona evidence ve confidence modeli yok
- Geliştirme:
  - `personaType`, `goals`, `frictions`, `evidenceRefs`, `confidence` alanları eklenmeli

## P17 — Scope Control Protocol
- Olgunluk: M2
- Eksik:
  - scope freeze ve overflow tespiti için alan yok
- Geliştirme:
  - `inScope`, `outOfScope`, `deferredItems`, `scopeRisk`, `scopeFreeze` alanları eklenmeli

---

# 3. UX & Design Protocols

## P20 — Information Architecture Protocol
- Olgunluk: M3
- Eksik:
  - sitemap ile screen tree ayrımı registry’de yok
  - admin/public surface ayrımı zorunlu değil
- Geliştirme:
  - `sitemap`, `screenTree`, `contentHierarchy`, `navigationPressurePoints` eklenmeli

## P21 — User Flow Protocol
- Olgunluk: M2
- Eksik:
  - flow step schema yok
  - happy path / error path ayrımı yok
- Geliştirme:
  - `flowId`, `entryStep`, `steps`, `decisionPoints`, `failurePaths` alanları eklenmeli

## P22 — Navigation System Protocol
- Olgunluk: M3
- Eksik:
  - desktop/tablet/mobile model ayrımı resmi değil
  - hybrid navigation sınıfı açık değil
- Geliştirme:
  - `desktopModel`, `tabletModel`, `mobileModel`, `menuItems`, `navDepth` eklenmeli

## P23 — Form Interaction Protocol
- Olgunluk: M2
- Eksik:
  - validation, error state, success state ve accessibility bağları eksik
- Geliştirme:
  - `fieldGroups`, `validationRules`, `errorPresentation`, `submitStates` eklenmeli

## P24 — Interaction Pattern Protocol
- Olgunluk: M2
- Eksik:
  - modal, drawer, table, CTA, stepper gibi pattern class’ları yok
- Geliştirme:
  - pattern taxonomy ve device-specific behavior eklenmeli

## P25 — Accessibility UX Protocol
- Olgunluk: M2
- Eksik:
  - landmark, focus, reduced motion ve aria hedefleri resmi değil
- Geliştirme:
  - `a11yGoals`, `interactionConstraints`, `requiredSemantics` eklenmeli

## P26 — Mobile UX Protocol
- Olgunluk: M3
- Eksik:
  - content priority ve table fallback modeli yok
- Geliştirme:
  - `layoutRules`, `touchRules`, `priorityContent`, `mobileWarnings` eklenmeli

## P27 — Tablet UX Protocol
- Olgunluk: M2
- Eksik:
  - tablet specific split-layout ve collapsible navigation kuralları yok
- Geliştirme:
  - `tabletLayoutRules`, `hybridNavigationRules`, `landscapeBehavior` eklenmeli

## P28 — Admin Experience Protocol
- Olgunluk: M2
- Eksik:
  - density/readability balance alanı yok
  - table/filter/action panel ilişkisi yok
- Geliştirme:
  - `moduleDensity`, `tableStrategy`, `bulkActionRules`, `roleSensitiveSurfaces` eklenmeli

## P29 — Automation UX Protocol
- Olgunluk: M2
- Eksik:
  - automation preview, dry-run, explainability ve risk hint alanları yok
- Geliştirme:
  - `automationType`, `userVisibility`, `dryRunSupport`, `riskHints` eklenmeli

## P30 — Visual Preference Protocol
- Olgunluk: M2
- Eksik:
  - liked/disliked patterns ayrımı resmi değil
  - confidence ve lock desteği yok
- Geliştirme:
  - `preferredStyles`, `avoidedStyles`, `strength`, `locked` eklenmeli

## P31 — Art Direction Protocol
- Olgunluk: M3
- Eksik:
  - style axis ve avoid list registry’de yok
- Geliştirme:
  - `styleAxis`, `brandMood`, `creativeBoundaries`, `avoidList` eklenmeli

## P32 — Color Token Protocol
- Olgunluk: M3
- Eksik:
  - semantic token sınıfları ve contrast evidence alanları resmi değil
- Geliştirme:
  - `semanticTokens`, `themeModes`, `contrastEvidence` eklenmeli

## P33 — Typography Protocol
- Olgunluk: M3
- Eksik:
  - display/body/mono family ve usage map tanımı yok
- Geliştirme:
  - `fontFamilies`, `scale`, `lineHeightRules`, `usageMap` eklenmeli

## P34 — Motion Protocol
- Olgunluk: M2
- Eksik:
  - motion purpose, reduced motion fallback ve timing tiers yok
- Geliştirme:
  - `motionClasses`, `timingTokens`, `reducedMotionFallbacks` eklenmeli

## P35 — Layout Rhythm Protocol
- Olgunluk: M2
- Eksik:
  - spacing scale, grid, section rhythm alanları yok
- Geliştirme:
  - `spacingScale`, `gridRules`, `sectionRhythm`, `contentDensity` eklenmeli

## P36 — Component Style Protocol
- Olgunluk: M2
- Eksik:
  - component variant naming, states ve token binding modeli yok
- Geliştirme:
  - `componentFamily`, `variants`, `stateMap`, `tokenBindings` eklenmeli

## P37 — Design Token Protocol
- Olgunluk: M3
- Eksik:
  - motion, radius, shadow token grupları registry’de görünmüyor
- Geliştirme:
  - `tokenPackId`, `version`, `colors`, `typography`, `spacing`, `radius`, `motion`, `shadow` eklenmeli

## P38 — Variation Candidate Protocol
- Olgunluk: M2
- Eksik:
  - candidate comparison ve reason summary yapısı yok
- Geliştirme:
  - `candidateId`, `comparisonAxes`, `reasonSummary`, `tradeoffs`, `recommendedFor` eklenmeli

---

# 4. Architecture & Code Protocols

## P40 — Business Model Protocol
- Olgunluk: M1
- Eksik:
  - tüm alanlar pratikte belirsiz
- Geliştirme:
  - `businessType`, `revenueModel`, `userSegments`, `coreValueExchange` eklenmeli

## P41 — Domain Model Protocol
- Olgunluk: M1
- Eksik:
  - bounded context, entity, value object, aggregate modeli yok
- Geliştirme:
  - `entities`, `relationships`, `invariants`, `boundedContexts` eklenmeli

## P42 — Backend Architecture Protocol
- Olgunluk: M1
- Eksik:
  - service topology, API surface, job model, state ownership yok
- Geliştirme:
  - `serviceMap`, `jobTypes`, `stateOwnership`, `integrationBoundaries` eklenmeli

## P43 — Frontend Architecture Protocol
- Olgunluk: M3
- Eksik:
  - render mode ve state strategy resmi minimum alan olarak yazılmamış
- Geliştirme:
  - `routeMap`, `componentTree`, `stateStrategy`, `renderRules` netleşmeli

## P44 — API Contract Protocol
- Olgunluk: M3
- Eksik:
  - request schema, response schema ve versioning kuralları açık minimum alan seti olarak yazılmalı
- Geliştirme:
  - `endpoints`, `requestSchemas`, `responseSchemas`, `errorSchemas`, `versioningRules` eklenmeli

## P45 — Data Schema Protocol
- Olgunluk: M2
- Eksik:
  - table/entity/store ayırımı yok
  - migration impact alanı yok
- Geliştirme:
  - `schemaObjects`, `indexes`, `retentionRules`, `migrationRisk` eklenmeli

## P46 — Auth Protocol
- Olgunluk: M2
- Eksik:
  - session-first vs JWT vs service token ayrımı registry’de yok
- Geliştirme:
  - `authMode`, `sessionContext`, `serviceTokenClaims`, `reviewTokenScope` eklenmeli

## P47 — Role & Permission Protocol
- Olgunluk: M2
- Eksik:
  - permission domain ve contextual guard yapısı yok
- Geliştirme:
  - `roles`, `permissions`, `scopeRules`, `contextualChecks` eklenmeli

## P48 — Workflow Protocol
- Olgunluk: M1
- Eksik:
  - workflow state, trigger, action, compensation mantığı yok
- Geliştirme:
  - `workflowId`, `states`, `transitions`, `sideEffects`, `compensations` eklenmeli

## P49 — Integration Action Protocol
- Olgunluk: M2
- Eksik:
  - external vendor trust level, data sharing scope ve fallback modeli yok
- Geliştirme:
  - `integrationType`, `vendorRef`, `dataBoundary`, `fallbackPlan` eklenmeli

## P50 — Code Patch Protocol
- Olgunluk: M3
- Eksik:
  - patch provenance, sideEffect class ve target artifact refs net değil
- Geliştirme:
  - `patchId`, `changeType`, `affectedArtifacts`, `affectedContracts`, `rationale`, `createdByAgentId` eklenmeli

## P51 — Artifact Manifest Protocol
- Olgunluk: M4
- Güçlü yan: ayrı belgeyle destekleniyor
- Eksik:
  - registry özetinde preview/release/rollback bağları görünmüyor
- Geliştirme:
  - `entryPoints`, `contractImpacts`, `qaCoverage`, `traceLinks` registry’ye taşınmalı

## P52 — External Dependency Protocol
- Olgunluk: M2
- Eksik:
  - dependency risk, SLA, approvalRequired ve version pin alanları yok
- Geliştirme:
  - `dependencyType`, `riskLevel`, `versionPin`, `approvalRequired`, `fallbackAvailable` eklenmeli

---

# 5. Runtime & Preview Protocols

## P60 — Build Protocol
- Olgunluk: M3
- Eksik:
  - build artifact ref, failure category, command ref ve duration bilgileri yok
- Geliştirme:
  - `buildId`, `status`, `command`, `artifactRefs`, `failureCategory`, `logRef` eklenmeli

## P61 — Runtime Start Protocol
- Olgunluk: M3
- Eksik:
  - health checks, port bindings, runtime mode resmi minimum alan seti değil
- Geliştirme:
  - `runtimeId`, `startCommand`, `portBindings`, `healthChecks`, `runtimeMode` eklenmeli

## P62 — Preview Sync Protocol
- Olgunluk: M3
- Eksik:
  - panel sync drift ve selected route/viewport alanları eksik
- Geliştirme:
  - `previewSessionId`, `availableRoutes`, `selectedRoute`, `viewportModes`, `lastRenderAt`, `syncStatus` eklenmeli

## P63 — Render Snapshot Protocol
- Olgunluk: M3
- Eksik:
  - layout integrity, interaction integrity ve snapshot type yok
- Geliştirme:
  - `renderId`, `routeRef`, `viewportId`, `captureRef`, `layoutIntegrity`, `interactionIntegrity`, `snapshotType` eklenmeli

## P64 — Panel Interaction Protocol
- Olgunluk: M1
- Eksik:
  - panel action taxonomy yok
  - user vs operator panel actions ayrımı yok
- Geliştirme:
  - `panelActionType`, `initiatedBy`, `targetSurface`, `result`, `linkedRefs` eklenmeli

---

# 6. QA & Validation Protocols

## P70 — Code Review Report Protocol
- Olgunluk: M2
- Eksik:
  - finding severity, blocking flag ve artifact refs yok
- Geliştirme:
  - `findings`, `severitySummary`, `blocking`, `artifactRefs` eklenmeli

## P71 — Static Analysis Report Protocol
- Olgunluk: M2
- Eksik:
  - rule ids, path refs, remediation hints yok
- Geliştirme:
  - `toolRef`, `violations`, `ruleIds`, `fileRefs`, `remediationHints` eklenmeli

## P72 — Responsive QA Protocol
- Olgunluk: M3
- Eksik:
  - viewport-specific issue formatı ve blocking criteria net değil
- Geliştirme:
  - `viewportFindings`, `criticalRoutes`, `layoutIntegritySummary`, `blockingThreshold` eklenmeli

## P73 — Accessibility QA Protocol
- Olgunluk: M3
- Eksik:
  - issue classes ve baseline result modeli resmi değil
- Geliştirme:
  - `baselineChecks`, `violations`, `focusIssues`, `contrastIssues`, `releaseBlocking` eklenmeli

## P74 — Performance QA Protocol
- Olgunluk: M2
- Eksik:
  - metric list, threshold ve percentile bilgisi yok
- Geliştirme:
  - `metrics`, `thresholds`, `routeSamples`, `regressionDelta` eklenmeli

## P75 — Security QA Protocol
- Olgunluk: M2
- Eksik:
  - secret scan, vuln scan, authz checks ve tenant checks ayrımı yok
- Geliştirme:
  - `scanClasses`, `findings`, `criticalCount`, `tenantIsolationChecks` eklenmeli

## P76 — Regression Report Protocol
- Olgunluk: M2
- Eksik:
  - previous baseline ref ve affected routes/artifacts yok
- Geliştirme:
  - `baselineRef`, `regressions`, `affectedArtifacts`, `affectedRoutes`, `severitySummary` eklenmeli

## P77 — Contract Test Report Protocol
- Olgunluk: M3
- Eksik:
  - contract version refs ve compatibility mode yok
- Geliştirme:
  - `contractRefs`, `compatibilityStatus`, `breakingDetected`, `evidenceRefs` eklenmeli

---

# 7. Governance, Audit & Control Protocols

## P80 — Policy Registry Protocol
- Olgunluk: M3
- Eksik:
  - enforcement source ve conflict priority band alanları yok
- Geliştirme:
  - `policyFamily`, `enforcementMode`, `subjects`, `triggerMoments`, `priorityBand` eklenmeli

## P81 — Policy Decision Protocol
- Olgunluk: M3
- Eksik:
  - evidence refs, approvalRequired, releaseImpact ve requiredActions alanları eksik
- Geliştirme:
  - `decision`, `severity`, `blocking`, `reasonSummary`, `evidenceRefs`, `requiredActions` eklenmeli

## P82 — Compliance Mapping Protocol
- Olgunluk: M2
- Eksik:
  - jurisdiction map, scope, evidence refs, escalation path yok
- Geliştirme:
  - `complianceScope`, `jurisdictions`, `controls`, `evidenceRefs`, `escalationRequired` eklenmeli

## P83 — Privacy Policy Protocol
- Olgunluk: M2
- Eksik:
  - data categories, retention, deletion and correction rules protokol düzeyinde yok
- Geliştirme:
  - `dataClasses`, `retentionRules`, `privacyDefaults`, `deletionSupport` eklenmeli

## P84 — Data Classification Protocol
- Olgunluk: M2
- Eksik:
  - class taxonomy, sensitivity band ve handling rules yok
- Geliştirme:
  - `classificationId`, `sensitivityBand`, `handlingRules`, `storageRestrictions` eklenmeli

## P85 — Audit Trail Protocol
- Olgunluk: M3
- Eksik:
  - integrity hash ve actor/subject standardı registry’de görünür değil
- Geliştirme:
  - `auditRecordId`, `actor`, `subject`, `payload`, `integrityHash`, `createdAt` eklenmeli

## P86 — Observability Protocol
- Olgunluk: M3
- Eksik:
  - trace/log/metric separation ve required correlation ids yok
- Geliştirme:
  - `traceContext`, `logEventType`, `metricPoints`, `resourceContext` eklenmeli

## P87 — Intervention Protocol
- Olgunluk: M3
- Eksik:
  - authority level, approval coupling ve execution status alanları registry’de yok
- Geliştirme:
  - `interventionId`, `actionType`, `authorityLevel`, `approvalRef`, `executionStatus`, `resultSummary` eklenmeli

## P88 — Rollback Protocol
- Olgunluk: M3
- Eksik:
  - safe point ve validation plan alanları registry’de yok
- Geliştirme:
  - `rollbackId`, `targetSnapshotId`, `rollbackScope`, `validationPlanRef`, `executionStatus` eklenmeli

## P89 — Approval Protocol
- Olgunluk: M3
- Eksik:
  - subject scope, approver rules, self-approval restriction yok
- Geliştirme:
  - `approvalId`, `subjectRef`, `requiredApprovers`, `status`, `selfApprovalAllowed`, `resolvedAt` eklenmeli

## P90 — Risk Score Protocol
- Olgunluk: M2
- Eksik:
  - numeric score, contributors ve release recommendation yapısı yok
- Geliştirme:
  - `riskScoreId`, `numericScore`, `riskBand`, `contributors`, `releaseRecommendation` eklenmeli

## P91 — Release Decision Protocol
- Olgunluk: M3
- Eksik:
  - linked preview/QA/approval evidence alanları yok
  - final decision sonuç kümesi net değil
- Geliştirme:
  - `releaseDecisionId`, `decision`, `blockingReasons`, `requiredNextActions`, `evidenceRefs` eklenmeli

---

# 8. Çapraz Boşluklar

Mevcut registry’de tekrar eden ortak eksikler:
- çoğu protokolde resmi lifecycle eksik
- çoğu protokolde `errorModes` tanımsız
- çoğu protokolde `evidenceRefs` yok
- çoğu protokolde `workspaceId`, `turnId`, `traceId` görünmüyor
- çoğu protokol için valid/invalid fixture zorunluluğu yazılı değil
- preview ve release bağları birçok protokolde yalnız ima düzeyinde

---

# 9. En Öncelikli Güçlendirme Listesi

İlk güçlendirilmesi gereken protokoller:
1. P01 Task Contract
2. P02 Task Graph
3. P10–P17 discovery grubu
4. P20–P24 UX çekirdeği
5. P44 API Contract
6. P45 Data Schema
7. P46 Auth
8. P60–P64 preview grubu
9. P72–P77 QA grubu
10. P81, P87, P88, P89, P91 governance çekirdeği

---

# 10. Sonuç
Mevcut protokol seti güçlü bir omurga veriyor; ancak protokollerin önemli bir bölümü isim ve amaç düzeyinden schema-ready düzeye çıkarılmalıdır. Özellikle discovery, UX, architecture, QA ve governance protokollerinde resmi minimum alan setleri, lifecycle ve evidence bağları eklenmelidir.
