# Platform Policy Families — PL-023 to PL-033

Bu belge SLA, analytics, experimentation, billing, licensing, prompt security, output safety, tenancy, compliance, change ve onboarding odaklı son 11 politika ailesini içerir.

---

## PL-023 — SLA, SLO & Support Policies
**Amaç:** Preview startup, turn completion, availability ve kullanıcı bildirim hedeflerini görünür kılmak.

**Temel Politikalar**
- SS-001 Preview Startup SLO
- SS-002 Turn Completion SLO
- SS-003 Availability Objective
- SS-004 User Notification on Maintenance

**Pass Criteria**
- Kritik servisler için zaman/hedef metrikleri tanımlıdır.
- Kesinti ve bakım durumlarında kullanıcı iletişimi planlıdır.
- SLO drift’leri review edilir.

**Failure Modes**
- No startup target
- No turn completion target
- Silent maintenance
- Untracked availability degradation

**Default Enforcement**
- allow_with_warning / require_review

---

## PL-024 — User Feedback & Analytics Policies
**Amaç:** Geri bildirim toplama ve analytics anonimleştirmeyi kontrollü hale getirmek.

**Temel Politikalar**
- UF-001 End-of-Turn Feedback Capture
- UF-002 Rejected Option Collection
- UF-003 Analytics Anonymization
- UF-004 Feedback Loop Closure

**Pass Criteria**
- Feedback toplama akışı vardır.
- Reddedilen seçenekler anlamlı sinyal olarak saklanır.
- Analytics verileri anonimleştirilir ve veri minimizasyonuna uyar.

**Failure Modes**
- Analytics privacy misuse
- No feedback capture
- Feedback ignored indefinitely
- Excessive personal telemetry

**Default Enforcement**
- warn / require_review / hard_block for privacy misuse

---

## PL-025 — A/B Testing & Experimentation Policies
**Amaç:** Deneylerin kontrollü, adil, istatistiksel ve geri çekilebilir olmasını sağlamak.

**Temel Politikalar**
- AB-001 Experiment Definition
- AB-002 Fair Assignment
- AB-003 Statistical Significance
- AB-004 Failed Experiment Auto-Retreat

**Pass Criteria**
- Her deneyin hipotezi ve başarı ölçütü vardır.
- Trafik dağılımı adildir.
- Başarısız deneyde otomatik geri çekilme kuralı tanımlıdır.

**Failure Modes**
- Undefined experiment
- Biased assignment
- No rollback for harmful experiment
- Weak evidence but hard rollout

**Default Enforcement**
- require_review / require_approval / hard_block

---

## PL-026 — Billing, Payment & Subscription Policies
**Amaç:** Kullanım ölçümü, plan sınırları, ödeme başarısızlığı ve erişim ilişkisini yönetmek.

**Temel Politikalar**
- BP-001 Usage Metering
- BP-002 Payment Failure Access
- BP-003 Free Tier Limit
- BP-004 Refund and Credit

**Pass Criteria**
- Usage events doğru ölçülür.
- Plan sınırları açık uygulanır.
- Payment failure durumunda erişim davranışı tanımlıdır.

**Failure Modes**
- Incorrect metering
- Missing access restriction logic
- Free tier abuse path
- Refund ambiguity

**Default Enforcement**
- allow / warn / turn_block / require_review

---

## PL-027 — Open Source & Licensing Policies
**Amaç:** Third-party dependency lisans uyumu ve repo lisans açıklığını korumak.

**Temel Politikalar**
- OL-001 Third-Party License Compliance
- OL-002 Repository License Declaration
- OL-003 Contribution Terms

**Pass Criteria**
- Dependency lisansları release ile uyumludur.
- Repo lisansı açıktır.
- Katkı koşulları tanımlıdır.

**Failure Modes**
- Incompatible license in release path
- Missing repository license
- Undefined contribution terms

**Default Enforcement**
- warn / release_hold / hard_block

---

## PL-028 — Prompt & Input Security Policies
**Amaç:** Zararlı girdi, prompt enjeksiyonu, system prompt sızıntısı ve input size risklerini azaltmak.

**Temel Politikalar**
- PI-001 Harmful Input Filtering
- PI-002 System Prompt Secrecy
- PI-003 Input Size Limit
- PI-004 Special Character Escaping

**Pass Criteria**
- Zararlı veya aşırı büyük girdiler kontrol edilir.
- System prompt ve gizli yönlendirmeler dışa sızdırılmaz.
- Escaping/sanitization kuralları uygulanır.

**Failure Modes**
- Prompt injection success path
- Oversized input causing instability
- Secret prompt leakage
- Unsafe escaping

**Default Enforcement**
- turn_block / hard_block

---

## PL-029 — Model Output Censorship & Safety Policies
**Amaç:** Yasaklı içerik kategorilerini ve güvenli output fallback davranışını enforce etmek.

**Temel Politikalar**
- MS-001 Prohibited Output Category
- MS-002 Output Moderation
- MS-003 Unsafe Output Fallback
- MS-004 Output Audit Retention

**Pass Criteria**
- Yasaklı içerikler engellenir veya güvenli fallback uygulanır.
- Moderation katmanı kritik üretim yüzeylerinde devrededir.
- Gereken durumlarda output denetim izi tutulur.

**Failure Modes**
- Unsafe content served
- Missing moderation path
- No fallback behavior
- No retention for regulated output cases

**Default Enforcement**
- turn_block / hard_block

---

## PL-030 — Multi-Tenancy & Isolation Policies
**Amaç:** Tenant bazlı veri, cache, preview ve runtime izolasyonunu korumak.

**Temel Politikalar**
- MT-001 Tenant Data Isolation
- MT-002 Fair Resource Allocation
- MT-003 Tenant Rate Limiting
- MT-004 Isolation Level Declaration

**Pass Criteria**
- Tenant verisi namespace ve auth düzeyinde ayrılmıştır.
- Preview plane tenant sınırını aşmaz.
- Shared cache veya storage convenience uğruna izolasyon zayıflatılmaz.

**Failure Modes**
- Cross-tenant cache leak
- Shared preview state risk
- Namespace confusion
- Missing tenant-aware rate controls

**Default Enforcement**
- require_review / hard_block

---

## PL-031 — Compliance Certification Policies
**Amaç:** Uyum kanıtları, kapsam eşleme ve breach notification readiness’ı korumak.

**Temel Politikalar**
- CC-001 Certification Scope Mapping
- CC-002 Evidence Retention
- CC-003 Regulation Adaptation Time
- CC-004 Compliance Breach Notification

**Pass Criteria**
- Hedef sertifikasyon kapsamı haritalanmıştır.
- Evidence retention planı vardır.
- Breach ve regülasyon uyum adımları tanımlıdır.

**Failure Modes**
- Missing evidence trail
- Undefined scope mapping
- No breach notification procedure
- Reg change adaptation blind spot

**Default Enforcement**
- require_review / require_approval / hard_block

---

## PL-032 — Change & Configuration Management Policies
**Amaç:** Change impact analysis, config approval, reversibility ve hotfix disiplinini korumak.

**Temel Politikalar**
- CM-001 Change Impact Analysis
- CM-002 Configuration Approval
- CM-003 Reversible Change
- CM-004 Emergency Hotfix Procedure

**Pass Criteria**
- Kritik değişiklikler impact analysis taşır.
- Config değişiklikleri onay zincirine uyar.
- Hotfix ve release path rollback düşünür.

**Failure Modes**
- Hotfix without rollback path
- Config mutation without approval
- Destructive schema change without review
- Missing change log

**Default Enforcement**
- require_review / require_approval / release_hold / hard_block

---

## PL-033 — Training & Onboarding Policies
**Amaç:** Privileged aktörlerin eğitim, yetkinlik ve simülasyon şartlarını korumak.

**Temel Politikalar**
- TO-001 Minimum Operator Training
- TO-002 Role-Based Competency
- TO-003 Documentation Readiness
- TO-004 Simulation Before Live Access

**Pass Criteria**
- Operator, approver ve security reviewer gibi roller için eğitim tabanı vardır.
- Simülasyon veya hazırlık eşiği olmadan canlı kritik eylem verilmez.
- Dokümantasyon erişilebilir durumdadır.

**Failure Modes**
- Privileged action by unprepared actor
- No simulation before live rollback/release tasks
- Missing onboarding baseline

**Default Enforcement**
- require_review / hard_block

---

## Uygulama Notu
Bu aileler doğrudan şu teknik yüzeylere bağlanır:
- observability and support dashboards
- analytics pipelines
- experimentation configs
- billing and plan checks
- license scans
- input gateway and moderation layer
- tenancy-aware auth and topology
- change management and hotfix workflows
- privileged actor auth and governance flows
