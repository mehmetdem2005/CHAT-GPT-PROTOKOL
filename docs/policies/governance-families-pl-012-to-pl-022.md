# Governance Policy Families — PL-012 to PL-022

Bu belge audit, observability, governance, deployment, incident, vendor, AI ve recovery odaklı politika ailelerini içerir.

---

## PL-012 — Auditability & Observability Policies
**Amaç:** Kritik kararların, error’ların, intervention’ların ve release hareketlerinin izlenebilir olmasını sağlamak.

**Temel Politikalar**
- AO-001 Audit Trail Completeness
- AO-002 Trace Correlation
- AO-003 Health Visibility
- AO-004 Decision Evidence

**Pass Criteria**
- Kritik eylemler audit event üretir.
- Trace ve log korelasyonu kurulabilir.
- Health ve diagnostics sinyalleri operasyonel görünürlüğe sahiptir.

**Failure Modes**
- Missing audit trail
- Uncorrelated critical errors
- Health blind spots
- No evidence for blocking decisions

**Default Enforcement**
- warn / require_review / release_hold

---

## PL-013 — Human Intervention & Governance Policies
**Amaç:** User lock, approval, override, rollback ve visible change summary disiplinini korumak.

**Temel Politikalar**
- HG-001 User Lock Respect
- HG-002 Explain Before Override
- HG-003 Rollback Availability
- HG-004 Major Structural Change Approval
- HG-005 User Visible Change Summary

**Pass Criteria**
- Kilitli kararlar sessizce bozulmaz.
- Override davranışı açıklanır.
- Rollback için güvenli nokta veya açık sınır bilgisi vardır.
- Major structural change approval gerektirir.

**Failure Modes**
- Silent lock bypass
- Override without rationale
- No rollback path
- Major structure change without approval

**Default Enforcement**
- require_user_choice / require_approval / turn_block

---

## PL-014 — Deployment & Release Management Policies
**Amaç:** Canary, blue-green, feature flag, rollback automation ve deployment approval zincirini korumak.

**Temel Politikalar**
- DR-001 Deployment Approval Chain
- DR-002 Canary Safety
- DR-003 Blue-Green Transition
- DR-004 Feature Flag Governance
- DR-005 Zero-Downtime Critical Surface

**Pass Criteria**
- Deployment mode release riskine uygun seçilir.
- Approval zinciri üretim dağıtımında zorunludur.
- Rollback readiness kayıtlıdır.
- Feature flag kullanımında sahiplik ve temizlik tanımlıdır.

**Failure Modes**
- Deploy without approval
- No rollback readiness
- Uncontrolled feature flag sprawl
- Unsafe production cutover

**Default Enforcement**
- require_approval / release_hold / hard_block

---

## PL-015 — Cost & Resource Management Policies
**Amaç:** Ajan çağrıları, preview kaynakları, storage ve pipeline maliyetini kontrol etmek.

**Temel Politikalar**
- CR-001 Agent Invocation Budget
- CR-002 Preview Runtime Resource Cap
- CR-003 Build Pipeline Cost
- CR-004 Storage Quota

**Pass Criteria**
- Preview ve build kaynakları sınırlandırılmıştır.
- Uzun koşan ve pahalı işler kontrolsüz büyümez.
- Storage artışı görünür ve sınırlıdır.

**Failure Modes**
- Unbounded preview pool usage
- Excessive agent invocations
- Artifact storage growth without cap
- Cost-heavy validation loops

**Default Enforcement**
- warn / require_review / turn_block

---

## PL-016 — Energy Efficiency & Sustainability Policies
**Amaç:** Gereksiz ajan işini ve boşta çalışan preview süreçlerini azaltmak.

**Temel Politikalar**
- ES-001 Redundant Agent Work Prevention
- ES-002 Auto-Teardown Idle Preview
- ES-003 Batch-Preferred Background Work

**Pass Criteria**
- Aynı işi tekrar eden ajan akışları azaltılır.
- Idle preview’lar kapatılır.
- Uygun yerlerde batch yaklaşımı kullanılır.

**Failure Modes**
- Zombie preview workers
- Duplicate generation loops
- Expensive always-on background processing

**Default Enforcement**
- advisory / warn

---

## PL-017 — Localization & Internationalization Policies
**Amaç:** Locale varsayımları, fallback dili, RTL ve bölgesel formatlamayı doğru yönetmek.

**Temel Politikalar**
- LI-001 Locale Default Behavior
- LI-002 Translation Fallback
- LI-003 RTL Support Readiness
- LI-004 Regional Formatting

**Pass Criteria**
- Varsayılan locale belirlenmiştir.
- Çeviri yoksa güvenli fallback vardır.
- RTL gereken bağlamlarda sistem bozulmaz.
- Tarih/para/sayı formatları bağlama uygundur.

**Failure Modes**
- Hard-coded locale assumptions
- Broken RTL layout
- Missing translation fallback
- Wrong currency/date formatting

**Default Enforcement**
- allow_with_warning / require_review

---

## PL-018 — Documentation & Knowledge Management Policies
**Amaç:** Ajan, protokol, politika ve release kararlarının dokümantasyon disiplinini korumak.

**Temel Politikalar**
- DK-001 Minimum Agent Documentation
- DK-002 Protocol Change Release Note
- DK-003 Decision Rationale Documentation

**Pass Criteria**
- Kritik ajan paketlerinde minimum docs vardır.
- Protocol/policy değişiklikleri release note taşır.
- Büyük kararlar rationale refs ile desteklenir.

**Failure Modes**
- Hidden change with no docs
- Missing release notes
- No rationale for structural decisions

**Default Enforcement**
- warn / require_review / release_hold

---

## PL-019 — AI Model Governance Policies
**Amaç:** Model versiyonu, prompt safety, explainability, bias ve tuning dataset güvenliğini korumak.

**Temel Politikalar**
- AM-001 Model Version Pinning
- AM-002 Prompt Injection Resilience
- AM-003 Explainable Model Decision
- AM-004 Bias Evaluation
- AM-005 Fine-Tuning Dataset Security

**Pass Criteria**
- Model versiyonları sabitlenebilir ve izlenebilir.
- Prompt ve fetched input güvenli sınırdan geçer.
- Kritik kararlar açıklanabilir sinyal üretir.
- Bias ve dataset güvenlik yüzeyleri review edilir.

**Failure Modes**
- Unpinned model drift
- Prompt injection path
- Opaque critical recommendation
- Unsafe training dataset handling

**Default Enforcement**
- require_review / require_approval / hard_block

---

## PL-020 — Third-Party Integration & Vendor Management Policies
**Amaç:** Vendor güvenliği, SLA yeterliliği, fallback ve veri paylaşım sınırlarını korumak.

**Temel Politikalar**
- TV-001 Pre-Integration Security Review
- TV-002 Vendor SLA Adequacy
- TV-003 Integration Fallback
- TV-004 Data Sharing Boundary

**Pass Criteria**
- Yeni vendor güvenlik ve SLA review’undan geçer.
- Kritik entegrasyonlarda fallback düşünülür.
- Outbound data boundary tanımlıdır.

**Failure Modes**
- Vendor added without review
- No fallback path
- Data oversharing to third party
- SLA mismatch for critical dependency

**Default Enforcement**
- require_review / require_approval / hard_block

---

## PL-021 — Incident & Problem Management Policies
**Amaç:** Incident seviyeleri, bildirim kanalları, postmortem ve RCA kapanış disiplinini korumak.

**Temel Politikalar**
- IP-001 Incident Severity Classification
- IP-002 Critical Notification Channel
- IP-003 Postmortem Required
- IP-004 RCA Closure

**Pass Criteria**
- P1–P4 sınıflandırması tutarlı uygulanır.
- Kritik olaylar doğru kanallara bildirilir.
- P1/P2 olaylar postmortem olmadan kapanmaz.
- RCA aksiyonları sahiplenilir.

**Failure Modes**
- Severity confusion
- Silent critical incident
- No postmortem
- RCA never closed

**Default Enforcement**
- require_review / release_hold in active incident contexts

---

## PL-022 — Backup, Recovery & Business Continuity Policies
**Amaç:** Backup, safe point, restore ve recovery readiness disiplinini korumak.

**Temel Politikalar**
- BC-001 Backup Frequency
- BC-002 Geographic Backup Redundancy
- BC-003 RPO/RTO Definition
- BC-004 Recovery Drill

**Pass Criteria**
- Kritik veriler için backup sıklığı tanımlıdır.
- Restore path doğrulanabilir.
- Rollback ve business continuity planı erişilebilirdir.

**Failure Modes**
- No recent backup
- Unvalidated restore path
- Missing safe point
- No recovery drill discipline

**Default Enforcement**
- require_review / require_approval / release_hold

---

## Uygulama Notu
Bu aileler doğrudan şu teknik yüzeylere bağlanır:
- audit events
- trace/log/metric mappings
- approval/intervention/rollback records
- deployment requests
- incident records
- backup and restore plans
- vendor metadata
- model configuration and invocation controls
