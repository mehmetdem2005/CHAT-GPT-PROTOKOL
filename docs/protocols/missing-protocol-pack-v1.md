# Missing Protocol Pack v1

Bu belge, ajan registry ve mimari belgelerde adı geçen ancak mevcut ana protocol registry içinde eksik veya ayrı authoritative tanım gerektiren protokolleri toplar.

## Amaç
- registry coverage boşluklarını kapatmak
- producer/consumer zincirlerini netleştirmek
- protocol v2 öncesi geçici ama authoritative bir köprü seti sağlamak

---

## MP-01 — Input Capture Protocol
**Purpose:** Ham kullanıcı cevaplarını, upload referanslarını ve seçimleri normalize edilmeden önce taşımak.
**Producers:** Studio UI, A03
**Consumers:** A06, A10
**Required Fields:** captureId, sourceSurface, rawInputs, uploadRefs, capturedAt, turnId
**Optional Fields:** locale, deviceHints, validationWarnings
**Error Modes:** invalid_input_shape, oversized_payload, missing_capture_context

## MP-02 — Uncertainty Protocol
**Purpose:** Eksik bilgi, düşük confidence ve clarification ihtiyacını standartlaştırmak.
**Producers:** A01, A06, A07
**Consumers:** A03, A60
**Required Fields:** uncertaintyId, subjectRefs, uncertaintyScore, blockingUnknowns, recommendedClarifications
**Optional Fields:** evidenceRefs, confidenceBands
**Error Modes:** missing_subjects, invalid_uncertainty_score

## MP-03 — Market Position Protocol
**Purpose:** Ürün fikrinin segment, rakip bağlamı ve değer önerisi çerçevesini taşımak.
**Producers:** A08
**Consumers:** A21, A22, A31
**Required Fields:** marketPositionId, targetSegments, valueHypotheses, differentiationNotes, riskNotes
**Optional Fields:** competitorRefs, evidenceRefs
**Error Modes:** ambiguous_positioning, missing_segment_context

## MP-04 — Validation Policy Protocol
**Purpose:** Form, workflow ve input validation kurallarını tek policy taşıyıcısında toplamak.
**Producers:** governance config, A53
**Consumers:** A14, A31, A41
**Required Fields:** validationPolicyId, ruleSets, fieldClasses, failurePresentationRules, escalationRules
**Optional Fields:** localeOverrides, accessibilityNotes
**Error Modes:** invalid_rule_set, unsupported_field_class

## MP-05 — Security Policy Protocol
**Purpose:** Güvenlik gereksinimlerini modül ve feature seviyesinde taşımak.
**Producers:** A52
**Consumers:** A36, A39, A46, A51
**Required Fields:** securityPolicyId, authRequirements, secretRules, inputSecurityRules, reviewTriggers
**Optional Fields:** vendorConstraints, environmentConstraints
**Error Modes:** incomplete_security_policy, missing_auth_boundary

## MP-06 — Brand Input Protocol
**Purpose:** Marka varlıklarını, tone ve görsel bağlam ipuçlarını normalize biçimde taşımak.
**Producers:** user upload flow, Studio UI
**Consumers:** A21, A29
**Required Fields:** brandInputId, assetRefs, toneHints, restrictedElements, sourceType
**Optional Fields:** colorHints, typographyHints, legalNotes
**Error Modes:** invalid_asset_ref, unsupported_brand_input

## MP-07 — Visual Consistency Report Protocol
**Purpose:** Görsel drift, token ihlali ve tutarsız component davranışlarını raporlamak.
**Producers:** A28
**Consumers:** A41, A43, A44, A48
**Required Fields:** visualConsistencyReportId, checkedSurfaces, driftFindings, severitySummary, recommendedFixes
**Optional Fields:** captureRefs, tokenRefs
**Error Modes:** missing_surface_refs, invalid_drift_classification

## MP-08 — Brand Mapping Protocol
**Purpose:** Marka girdisinin design token ve art direction sistemine nasıl eşlendiğini taşımak.
**Producers:** A29
**Consumers:** A31, A33
**Required Fields:** brandMappingId, brandInputRef, tokenOverrides, preservedConstraints, mappingSummary
**Optional Fields:** rejectedMappings, legalApprovals
**Error Modes:** unsafe_brand_override, missing_brand_input_ref

## MP-09 — Admin Module Protocol
**Purpose:** Admin modülünün ekran grupları, erişim yüzeyleri ve artifact kapsamını tanımlamak.
**Producers:** A37
**Consumers:** A41, A47, A49
**Required Fields:** adminModuleId, moduleSections, permissionRefs, routeRefs, artifactRefs
**Optional Fields:** bulkActionRules, auditRequirements
**Error Modes:** missing_permission_refs, invalid_admin_route

## MP-10 — Automation Runtime Protocol
**Purpose:** Automation builder çıktılarının runtime davranışını, trigger-action yürütmesini ve güvenli çalışma kurallarını taşımak.
**Producers:** A38
**Consumers:** A40, A46, A47
**Required Fields:** automationRuntimeId, workflowRefs, triggerModel, actionModel, failureHandling, safetyMode
**Optional Fields:** dryRunSupport, auditRefs
**Error Modes:** invalid_workflow_ref, unsafe_action_path, missing_failure_handling

## MP-11 — Code Snapshot Protocol
**Purpose:** Belirli bir turn veya patch sonrası codebase snapshot bağını standartlaştırmak.
**Producers:** A40, A42
**Consumers:** A41, A46, A48
**Required Fields:** codeSnapshotId, snapshotRef, createdAt, turnRef, artifactRefs, integrityHash
**Optional Fields:** baseSnapshotRef, diffSummary
**Error Modes:** snapshot_not_found, integrity_mismatch

---

## Uygulama Kuralı
Bu protokoller geçici not değil authoritative bridge set olarak düşünülmelidir. Registry v2 çıktığında kimlikleri korunmalı, gerekiyorsa P08/P09/P5x/P9x bandına taşınmalıdır.
