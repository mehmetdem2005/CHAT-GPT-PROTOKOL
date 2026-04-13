# Core Policy Families — PL-001 to PL-011

Bu belge çekirdek ürün, UX, güvenlik, mimari, runtime ve QA odaklı ilk 11 politika ailesini içerir.

---

## PL-001 — Agent Behavior Policies
**Amaç:** Ajanların contract-first, izlenebilir, müdahale edilebilir ve minimum gerekli değişiklik ilkesiyle çalışmasını sağlamak.

**Temel Politikalar**
- PB-001 Contract-First Behavior
- PB-002 No Hidden Cross-Module Assumption
- PB-003 Deterministic Traceability
- PB-004 Human Interruptibility
- PB-005 Safe Regeneration
- PB-006 Minimal Necessary Change

**Pass Criteria**
- Her ajan girdi ve çıktılarını resmi protokoller üzerinden taşır.
- Ajanlar sessiz yapısal varsayımlarla başka modülleri mutasyona uğratmaz.
- Üretilen patch’ler gerekçeli ve izlenebilir olur.

**Failure Modes**
- Hidden dependency
- Lock bypass
- Unexplained patch
- Non-deterministic task output in controlled flows

**Default Enforcement**
- warn -> review -> turn_block

---

## PL-002 — Product Quality Policies
**Amaç:** Üretilen sistemin hedef ürüne, kapsam sınırına ve non-functional beklentilere uymasını sağlamak.

**Temel Politikalar**
- PQ-001 Goal Alignment
- PQ-002 Scope Discipline
- PQ-003 Non-Functional Requirements Coverage
- PQ-004 Progressive Delivery

**Pass Criteria**
- Çıktı ürün niyetine açıkça bağlanır.
- MVP kapsamı faz 2 ve backlog ile karışmaz.
- Temel performans, güvenlik, responsive davranış ve kalite ölçütleri tanımlıdır.

**Failure Modes**
- Scope creep
- Product intent drift
- Missing NFR baseline
- Overbuilt initial solution

**Default Enforcement**
- warn / review / release_hold

---

## PL-003 — UX Policies
**Amaç:** Kullanıcıya açıklanabilir, zengin seçenekli, güvenli ve cihaz uyumlu deneyim sunmak.

**Temel Politikalar**
- UX-001 User Choice Richness
- UX-002 Ask Before Lock
- UX-003 Flow Clarity
- UX-004 Mobile-First Interaction Safety
- UX-005 Dangerous Action Friction
- UX-006 Admin Density Balance
- UX-007 Automation Explainability

**Pass Criteria**
- Sistem gerekli anlarda seçenek sunar.
- Kritik kararlar kilitlenmeden önce görünür ve anlaşılırdır.
- Mobil etkileşimler temel kullanım eşiğini karşılar.
- Admin ve automation yüzeylerinde bilgi yoğunluğu ile okunabilirlik dengelenir.

**Failure Modes**
- Forced hidden choices
- Unsafe destructive action flow
- Mobile unusability
- Unclear automation consequences

**Default Enforcement**
- allow / allow_with_warning / require_user_choice / require_review

---

## PL-004 — Visual Design Policies
**Amaç:** Görsel kaliteyi, kontrastı, motion amaçlılığını ve sistem tutarlılığını korumak.

**Temel Politikalar**
- VD-001 Non-Repetitive Typography
- VD-002 Semantic Color
- VD-003 Contrast Safety
- VD-004 Motion With Purpose
- VD-005 Reduced Motion Respect
- VD-006 Design System Consistency
- VD-007 Device-Specific Aesthetic Adaptation

**Pass Criteria**
- Font seçimi tekrarcı ve düşük kalite kalıplara saplanmaz.
- Renk sistemi semantik amaç taşır.
- Motion dekor değil anlam destekleyici olarak kullanılır.
- Görsel sistem cihaz bazlı kırılmaz.

**Failure Modes**
- Low contrast
- Motion gimmicks
- Token inconsistency
- Repetitive cliché visual stack

**Default Enforcement**
- warn / review / release_warning

---

## PL-005 — Accessibility Policies
**Amaç:** Erişilebilirlik baseline’ını teknik ve deneyim düzeyinde zorunlu kılmak.

**Temel Politikalar**
- AX-001 Keyboard Accessibility
- AX-002 Screen Reader Semantics
- AX-003 Focus Visibility
- AX-004 Form Error Accessibility
- AX-005 Minimum Accessibility Baseline

**Pass Criteria**
- Klavye ile temel kullanım mümkündür.
- Semantik yapı ve focus görünürlüğü sağlanır.
- Formlar erişilebilir etiket ve hata geri bildirimi taşır.
- Kontrast ve reduced motion eşiği göz ardı edilmez.

**Failure Modes**
- Hidden focus
- Landmark missing
- Contrast failure
- Broken form labeling

**Default Enforcement**
- warn / turn_block / release_hold

---

## PL-006 — Security Policies
**Amaç:** Auth, authorization, secret handling, input validation ve session güvenliğini enforce etmek.

**Temel Politikalar**
- SC-001 Authentication Required
- SC-002 Authorization Boundary
- SC-003 Secret Handling
- SC-004 Input Validation
- SC-005 Output Encoding & Exposure
- SC-006 Session Safety
- SC-007 External Integration Safety
- SC-008 Least Privilege
- SC-009 Security Review on Critical Change

**Pass Criteria**
- Hassas aksiyonlar doğrulanmış kimlik gerektirir.
- Role ve scope sınırları aşılmaz.
- Secret’lar preview veya frontend yüzeyine sızmaz.
- Zararlı girdi yolları filtrelenir.

**Failure Modes**
- Authz bypass
- Secret exposure
- Injection path
- Unsafe session persistence

**Default Enforcement**
- hard_block

---

## PL-007 — Privacy & Data Policies
**Amaç:** Veri minimizasyonu, hassas veri sınıflandırması ve privacy by default yaklaşımını zorunlu kılmak.

**Temel Politikalar**
- PD-001 Data Minimization
- PD-002 Sensitive Data Classification
- PD-003 Retention Definition
- PD-004 Deletion & Correction Capability
- PD-005 Privacy by Default

**Pass Criteria**
- Şema ve analytics payload’larında gereksiz veri tutulmaz.
- Hassas alanlar sınıflandırılır.
- Saklama ve silme davranışı tanımlanır.

**Failure Modes**
- Undefined retention
- Sensitive field misuse
- Excessive analytics capture
- Missing delete/correct path

**Default Enforcement**
- review / approval / hard_block

---

## PL-008 — Compliance & Legal Routing Policies
**Amaç:** Hukuki belirsizlik, sektör riski ve jurisdiction farklarını doğru review zincirine yönlendirmek.

**Temel Politikalar**
- CL-001 Jurisdiction Routing
- CL-002 Legal Uncertainty Escalation
- CL-003 High-Risk Domain Review
- CL-004 Claims Moderation

**Pass Criteria**
- Regülasyon duyarlı alanlar doğru review hattına düşer.
- Belirsiz hukuki alanlarda otomatik kesin karar verilmez.
- High-risk vertical’larda manual review zorunlu tutulur.

**Failure Modes**
- Unsupported legal assumption
- Missing jurisdiction mapping
- Unsafe product/legal claim generation

**Default Enforcement**
- require_review / require_approval / hard_block

---

## PL-009 — Architecture & Contract Policies
**Amaç:** Protocol, schema, versioning ve artifact ownership disiplinini korumak.

**Temel Politikalar**
- AC-001 Protocol Compliance
- AC-002 Versioned Contract
- AC-003 Artifact Ownership
- AC-004 Patch Explainability
- AC-005 No Silent Breaking Change

**Pass Criteria**
- Contract değişiklikleri versioned ve açıklanmış olur.
- Patch’lerin hangi artifact ve contract’ı etkilediği nettir.
- Sessiz breaking change yapılmaz.

**Failure Modes**
- Contract drift
- Manifest inconsistency
- Undocumented breaking API change
- Unowned artifact mutation

**Default Enforcement**
- turn_block / release_hold

---

## PL-010 — Runtime & Reliability Policies
**Amaç:** Health, timeout, retry safety ve preview/runtime istikrarını korumak.

**Temel Politikalar**
- RR-001 Health Check
- RR-002 Timeout
- RR-003 Retry Safety
- RR-004 Graceful Failure
- RR-005 Preview Stability

**Pass Criteria**
- Runtime health doğrulanır.
- Retry destructive side-effect yaratmaz.
- Preview plane yoğun hata durumunda degrade veya durdurma moduna geçebilir.

**Failure Modes**
- Endless retry loops
- Preview crash loops
- Missing health checks
- Unbounded runtimes

**Default Enforcement**
- warn / review / release_hold / rollback_recommended

---

## PL-011 — QA & Release Policies
**Amaç:** Release kararını zorunlu kalite, güvenlik, accessibility ve contract kapılarına bağlamak.

**Temel Politikalar**
- QR-001 Mandatory QA Gate
- QR-002 Regression Protection
- QR-003 Contract Integrity Gate
- QR-004 Critical Security Gate
- QR-005 Accessibility Gate
- QR-006 Release Risk Threshold
- QR-007 No Preview No Release

**Pass Criteria**
- Critical QA ve security gate’leri geçilmeden release ilerlemez.
- Preview yoksa release yoktur.
- Regression, contract break ve blocking a11y failures release’i durdurur.

**Failure Modes**
- Release despite failing contract tests
- Accessibility block ignored
- No preview candidate
- Critical regression accepted

**Default Enforcement**
- release_hold / hard_block

---

## Uygulama Notu
Bu aileler doğrudan şu teknik yüzeylere bağlanır:
- task contracts
- task graphs
- preview diagnostics
- QA reports
- API contracts
- auth guards
- deployment requests
- release gates
