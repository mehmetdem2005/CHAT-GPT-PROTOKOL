# Policy Registry

Bu belge, sistemde tanımlı tüm politika aileleri için resmi registry özeti sağlar.

## Registry Alanları
Her politika ailesi en az şu alanlarla düşünülmelidir:
- `policyId`
- `policyFamily`
- `title`
- `objective`
- `enforcementMode`
- `defaultSeverityBand`
- `primarySubjects`
- `primaryEnforcementSources`
- `passCriteria`
- `failureModes`
- `auditRequired`
- `releaseRelevant`

## Enforcement Mode Türleri
- `advisory`
- `warn`
- `soft_block`
- `approval_gate`
- `hard_block`
- `release_hold`

## Priority Bands
- `band_1_hard_safety`
- `band_2_release_critical`
- `band_3_governance_lock`
- `band_4_user_choice`
- `band_5_quality_warning`
- `band_6_heuristic_preference`

## Registry

### PL-001 — Agent Behavior Policies
- Objective: Ajanların contract-first, izlenebilir ve sınırlarına sadık çalışmasını sağlamak
- Enforcement: soft_block / hard_block bağlama göre
- Subjects: task contracts, task graphs, agent outputs, code patches
- Release Relevant: yes
- Audit Required: major/critical ihlallerde evet

### PL-002 — Product Quality Policies
- Objective: Üretilen çıktının ürün amacına ve kalite beklentilerine uymasını sağlamak
- Enforcement: warn / release_hold
- Subjects: requirements, preview sessions, QA reports, release candidates
- Release Relevant: yes
- Audit Required: release-impacting durumlarda evet

### PL-003 — UX Policies
- Objective: Kullanıcıya zengin seçim, açıklanabilir akış ve güvenli etkileşim sunmak
- Enforcement: advisory / warn / require_user_choice
- Subjects: option selections, navigation, interaction patterns, preview sessions
- Release Relevant: sometimes
- Audit Required: lock ve major conflict durumlarında evet

### PL-004 — Visual Design Policies
- Objective: Görsel kalite, kontrast ve motion amaçlılığını korumak
- Enforcement: warn / review
- Subjects: visual direction, token pack, rendered preview
- Release Relevant: yes when accessibility or release quality is affected
- Audit Required: usually no, major release-impacting ihlallerde yes

### PL-005 — Accessibility Policies
- Objective: Minimum erişilebilirlik baseline’ını zorunlu kılmak
- Enforcement: soft_block / release_hold
- Subjects: rendered preview, forms, navigation, release candidates
- Release Relevant: yes
- Audit Required: blocking failures için yes

### PL-006 — Security Policies
- Objective: Auth, authorization, validation ve secret handling güvenliğini korumak
- Enforcement: hard_block
- Subjects: auth actions, deployments, preview sessions, API contracts, integrations
- Release Relevant: yes
- Audit Required: yes

### PL-007 — Privacy & Data Policies
- Objective: Veri minimizasyonu ve privacy by default yaklaşımını enforce etmek
- Enforcement: review / approval / hard_block
- Subjects: schemas, analytics payloads, manifests, API contracts
- Release Relevant: yes
- Audit Required: yes

### PL-008 — Compliance & Legal Routing Policies
- Objective: Jurisdiction ve hukuki belirsizlikleri doğru review akışına yönlendirmek
- Enforcement: review / approval / hard_block
- Subjects: legal-sensitive features, releases, product decisions
- Release Relevant: yes
- Audit Required: yes

### PL-009 — Architecture & Contract Policies
- Objective: Protocol, schema ve versioning disiplinini korumak
- Enforcement: soft_block / release_hold
- Subjects: task contracts, graphs, contracts, schemas, patches, manifests
- Release Relevant: yes
- Audit Required: yes for major breaking changes

### PL-010 — Runtime & Reliability Policies
- Objective: Health, timeout, retry safety ve preview stability’yi korumak
- Enforcement: warn / review / release_hold
- Subjects: preview sessions, runtime instances, route validations, deployments
- Release Relevant: yes
- Audit Required: major runtime failures için yes

### PL-011 — QA & Release Policies
- Objective: Mandatory QA gate ve release quality threshold’larını korumak
- Enforcement: release_hold / hard_block
- Subjects: QA reports, preview sessions, release candidates, deployment requests
- Release Relevant: yes
- Audit Required: yes

### PL-012 — Auditability & Observability Policies
- Objective: Audit trail ve traceability eksiksizliğini korumak
- Enforcement: warn / review / release_hold
- Subjects: audit events, traces, logs, metrics, incidents
- Release Relevant: yes
- Audit Required: policy itself governs audit integrity

### PL-013 — Human Intervention & Governance Policies
- Objective: User lock, approval, rollback ve override disiplinini korumak
- Enforcement: require_user_choice / require_approval / turn_block
- Subjects: locks, approvals, rollbacks, intervention events
- Release Relevant: yes
- Audit Required: yes

### PL-014 — Deployment & Release Management Policies
- Objective: Release, canary, blue-green ve rollback güvenliğini korumak
- Enforcement: require_approval / release_hold / hard_block
- Subjects: deployments, release candidates, pipeline runs
- Release Relevant: yes
- Audit Required: yes

### PL-015 — Cost & Resource Management Policies
- Objective: Ajan, preview, storage ve pipeline tüketimini yönetmek
- Enforcement: warn / review / turn_block
- Subjects: task graphs, preview sessions, storage usage, pipeline runs
- Release Relevant: sometimes
- Audit Required: usually no, quota incidents forensics için yes

### PL-016 — Energy Efficiency & Sustainability Policies
- Objective: Gereksiz iş ve boşta çalışan runtime tüketimini azaltmak
- Enforcement: advisory / warn
- Subjects: preview sessions, task graphs, scheduled jobs
- Release Relevant: low
- Audit Required: no

### PL-017 — Localization & Internationalization Policies
- Objective: Locale, fallback dili, RTL ve formatlama kurallarını korumak
- Enforcement: warn / review
- Subjects: rendered preview, locale config, option selection outputs
- Release Relevant: medium
- Audit Required: no

### PL-018 — Documentation & Knowledge Management Policies
- Objective: Ajan, protokol ve release dokümantasyonunu güncel tutmak
- Enforcement: warn / release_hold
- Subjects: agent packages, protocol changes, policy changes, release packages
- Release Relevant: yes
- Audit Required: release and governance changes for yes

### PL-019 — AI Model Governance Policies
- Objective: Model version, prompt safety, bias ve explainability disiplinini korumak
- Enforcement: review / approval / hard_block
- Subjects: model invocations, agent configs, datasets, recommendations
- Release Relevant: yes
- Audit Required: yes

### PL-020 — Third-Party Integration & Vendor Management Policies
- Objective: Vendor güvenliği, fallback ve veri paylaşım sınırlarını korumak
- Enforcement: review / approval / hard_block
- Subjects: integrations, external dependencies, vendor onboarding
- Release Relevant: yes
- Audit Required: yes

### PL-021 — Incident & Problem Management Policies
- Objective: Severity, notification, postmortem ve RCA disiplinini korumak
- Enforcement: review / release_hold
- Subjects: incidents, escalations, postmortems
- Release Relevant: yes in active incident states
- Audit Required: yes for P1/P2

### PL-022 — Backup, Recovery & Business Continuity Policies
- Objective: Backup freshness, safe point ve restore readiness’ı korumak
- Enforcement: review / approval / release_hold
- Subjects: rollback plans, backups, restore plans, release candidates
- Release Relevant: yes
- Audit Required: yes

### PL-023 — SLA, SLO & Support Policies
- Objective: Preview startup, turn completion ve availability hedeflerini izlemek
- Enforcement: warn / review
- Subjects: preview sessions, turn states, service health summaries
- Release Relevant: medium
- Audit Required: usually no

### PL-024 — User Feedback & Analytics Policies
- Objective: Feedback collection ve analytics anonimleştirmeyi korumak
- Enforcement: warn / review / hard_block for privacy misuse
- Subjects: turn summaries, analytics events, feedback flows
- Release Relevant: medium
- Audit Required: privacy-sensitive analytics ihlallerinde yes

### PL-025 — A/B Testing & Experimentation Policies
- Objective: Deneylerin kontrollü, adil ve geri çekilebilir olmasını sağlamak
- Enforcement: review / approval / hard_block
- Subjects: experiment configs, traffic assignments, release candidates
- Release Relevant: yes
- Audit Required: yes for production experiments

### PL-026 — Billing, Payment & Subscription Policies
- Objective: Kullanım ölçümü, failed payment handling ve plan limitlerini korumak
- Enforcement: allow / warn / turn_block / review
- Subjects: usage events, plan access, billing actions
- Release Relevant: medium
- Audit Required: billing-sensitive flows for yes

### PL-027 — Open Source & Licensing Policies
- Objective: Lisans uyumu ve katkı hukuku tarafını temiz tutmak
- Enforcement: warn / release_hold / hard_block
- Subjects: dependencies, release packages, repo metadata
- Release Relevant: yes
- Audit Required: yes for release blockers

### PL-028 — Prompt & Input Security Policies
- Objective: Zararlı girdi, prompt sızıntısı ve injection riskini azaltmak
- Enforcement: turn_block / hard_block
- Subjects: user input, fetched external text, model invocation setup
- Release Relevant: yes
- Audit Required: yes

### PL-029 — Model Output Censorship & Safety Policies
- Objective: Yasaklı çıktı kategorileri ve güvenli fallback davranışını enforce etmek
- Enforcement: turn_block / hard_block
- Subjects: generated text, option copy, recommendations, template content
- Release Relevant: yes
- Audit Required: yes for blocked unsafe outputs

### PL-030 — Multi-Tenancy & Isolation Policies
- Objective: Tenant bazlı veri ve runtime izolasyonunu korumak
- Enforcement: review / hard_block
- Subjects: preview sessions, storage namespace, cache strategy, auth actions, topology config
- Release Relevant: yes
- Audit Required: yes

### PL-031 — Compliance Certification Policies
- Objective: Uyum kanıtı, kapsam ve breach notification readiness’ı korumak
- Enforcement: review / approval / hard_block
- Subjects: compliance evidence, releases, policy changes
- Release Relevant: yes
- Audit Required: yes

### PL-032 — Change & Configuration Management Policies
- Objective: Impact analysis, config approval ve reversible change disiplinini korumak
- Enforcement: review / approval / release_hold / hard_block
- Subjects: config changes, schema changes, deployments, hotfixes
- Release Relevant: yes
- Audit Required: yes

### PL-033 — Training & Onboarding Policies
- Objective: Yetkili aktörlerin eğitim ve yetkinlik şartlarını korumak
- Enforcement: review / hard_block
- Subjects: operator actions, approval actions, rollback execution actions
- Release Relevant: indirectly yes
- Audit Required: yes for privileged actions
