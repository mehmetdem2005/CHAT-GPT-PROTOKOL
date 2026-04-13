# Protocol Registry v1

Bu belge, sistemde kullanılan resmi protokollerin ilk kayıt defteridir.

## 1. Global Protokol Kuralları
Her protokol aşağıdaki alanlarla tanımlanır:
- `protocolId`
- `protocolName`
- `version`
- `category`
- `purpose`
- `producers`
- `consumers`
- `requiredFields`
- `optionalFields`
- `validationRules`
- `lifecycleRules`
- `errorModes`

### Ortak envelope alanları
Mümkün olan tüm protokoller şu ortak alanları taşımaya teşvik edilir:
- `protocolVersion`
- `messageId`
- `traceId`
- `turnId`
- `timestamp`
- `producerId`
- `payload`

### Ortak durum değerleri
- `pending`
- `accepted`
- `running`
- `blocked`
- `awaiting_input`
- `awaiting_approval`
- `completed`
- `failed`
- `rolled_back`

### Protokol sınıfları
- Core Envelope Protocols
- Discovery & Decision Protocols
- UX & Design Protocols
- Architecture & Code Protocols
- Runtime & Preview Protocols
- QA & Validation Protocols
- Governance & Audit Protocols

---

## 2. Core Envelope Protocols
### P01 — Task Contract Protocol
Amaç: Bir ajana resmi görev atamak.

Required fields:
- `taskId`
- `taskType`
- `targetAgentId`
- `priority`
- `inputRefs`
- `constraints`
- `expectedOutputs`
- `deadlineMode`

Optional fields:
- `parentTaskId`
- `blockingDependencies`
- `riskHints`
- `approvalHints`

Error modes:
- `invalid_target`
- `missing_dependencies`
- `invalid_constraints`

### P02 — Task Graph Protocol
Amaç: Bir turun veya üretim evresinin görev ağacını tanımlamak.

Required fields:
- `graphId`
- `rootTaskId`
- `nodes`
- `edges`
- `criticalPath`

Error modes:
- `cycle_detected`
- `orphan_node`
- `missing_root`

### P03 — Turn State Protocol
Amaç: Bir turun anlık durumunu, bekleyen kullanıcı girdisini ve tamamlanan adımları taşımak.

Required fields:
- `turnId`
- `turnNumber`
- `stage`
- `status`
- `completedTasks`
- `pendingTasks`
- `awaitingUserInput`

Optional fields:
- `previewStatus`
- `approvalStatus`
- `rollbackAvailable`

Error modes:
- `invalid_stage`
- `stale_state`

### P04 — Decision Log Protocol
Amaç: Kullanıcı veya ajan kararlarını append-only şekilde kayıt altına almak.

Required fields:
- `decisionId`
- `decisionType`
- `madeBy`
- `reason`
- `selectedOption`
- `affectedArtifacts`

### P05 — Decision Memory Protocol
Amaç: Geçerli kararların ve lock’ların okunabilir hafızasını taşımak.

Required fields:
- `memoryId`
- `lockedChoices`
- `activePreferences`
- `rejectedOptions`
- `versionedSnapshots`

### P06 — Event Contract Protocol
Amaç: Ajanlar arası olay yayınlarında ortak event zarfını tanımlamak.

Required fields:
- `eventId`
- `eventName`
- `eventVersion`
- `occurredAt`
- `producerId`
- `traceId`
- `payload`

Error modes:
- `invalid_event_name`
- `payload_schema_mismatch`

### P07 — Error Envelope Protocol
Amaç: Tüm hata döngülerini standartlaştırmak.

Required fields:
- `errorId`
- `code`
- `message`
- `sourceAgentId`
- `retryable`
- `severity`

Optional fields:
- `field`
- `suggestedAction`
- `relatedTaskId`

---

## 3. Discovery & Decision Protocols
### P10 — User Intent Protocol
### P11 — Discovery Summary Protocol
### P12 — Requirements Capture Protocol
### P13 — Structured Requirements Protocol
### P14 — Clarification Plan Protocol
### P15 — Feature Priority Protocol
### P16 — Persona Protocol
### P17 — Scope Control Protocol

Bu grup ürün niyeti, gereksinim toplama, yapılandırma ve kapsam kontrolü için kullanılır.

---

## 4. UX & Design Protocols
### P20 — Information Architecture Protocol
### P21 — User Flow Protocol
### P22 — Navigation System Protocol
### P23 — Form Interaction Protocol
### P24 — Interaction Pattern Protocol
### P25 — Accessibility UX Protocol
### P26 — Mobile UX Protocol
### P27 — Tablet UX Protocol
### P28 — Admin Experience Protocol
### P29 — Automation UX Protocol
### P30 — Visual Preference Protocol
### P31 — Art Direction Protocol
### P32 — Color Token Protocol
### P33 — Typography Protocol
### P34 — Motion Protocol
### P35 — Layout Rhythm Protocol
### P36 — Component Style Protocol
### P37 — Design Token Protocol
### P38 — Variation Candidate Protocol

Bu grup IA, UX, görsel sistem ve design token omurgasını tanımlar.

---

## 5. Architecture & Code Protocols
### P40 — Business Model Protocol
### P41 — Domain Model Protocol
### P42 — Backend Architecture Protocol
### P43 — Frontend Architecture Protocol
### P44 — API Contract Protocol
### P45 — Data Schema Protocol
### P46 — Auth Protocol
### P47 — Role & Permission Protocol
### P48 — Workflow Protocol
### P49 — Integration Action Protocol
### P50 — Code Patch Protocol
### P51 — Artifact Manifest Protocol
### P52 — External Dependency Protocol

Özellikle P50 ve P51 kod üreten ajanlar için zorunlu çekirdektir.

---

## 6. Runtime & Preview Protocols
### P60 — Build Protocol
### P61 — Runtime Start Protocol
### P62 — Preview Sync Protocol
### P63 — Render Snapshot Protocol
### P64 — Panel Interaction Protocol

Bu grup build, runtime, route, preview ve panel etkileşim omurgasını taşır.

---

## 7. QA & Validation Protocols
### P70 — Code Review Report Protocol
### P71 — Static Analysis Report Protocol
### P72 — Responsive QA Protocol
### P73 — Accessibility QA Protocol
### P74 — Performance QA Protocol
### P75 — Security QA Protocol
### P76 — Regression Report Protocol
### P77 — Contract Test Report Protocol

---

## 8. Governance, Audit & Control Protocols
### P80 — Policy Registry Protocol
### P81 — Policy Decision Protocol
### P82 — Compliance Mapping Protocol
### P83 — Privacy Policy Protocol
### P84 — Data Classification Protocol
### P85 — Audit Trail Protocol
### P86 — Observability Protocol
### P87 — Intervention Protocol
### P88 — Rollback Protocol
### P89 — Approval Protocol
### P90 — Risk Score Protocol
### P91 — Release Decision Protocol

---

## 9. Zorunlu Protokol Akışları
### Kullanıcıdan gereksinim toplama
P10 -> P11 -> P12 -> P13 -> P14 -> P03/P05

### UX ve tasarım
P13/P16 -> P20 -> P21 -> P22/P23/P24 -> P25/P26/P27 -> P31 -> P32/P33/P34/P35/P36 -> P37 -> P38

### Üretim
P13/P15/P17 -> P43/P42 -> P41/P45/P46/P47 -> P44/P48/P49 -> P50/P51/P52 -> P60/P61

### Preview ve doğrulama
P61 -> P62 -> P63 -> P70/P72/P73/P74/P75/P77 -> P76

### Governance
P80 -> P81 -> P82/P83/P84 -> P85/P86 -> P87/P88/P89/P90 -> P91

---

## 10. Minimum Çekirdek Protokol Seti
İlk çalışan çekirdek için minimum gerekli protokoller:
- P01
- P03
- P04
- P05
- P10
- P11
- P12
- P13
- P20
- P22
- P30
- P31
- P32
- P33
- P37
- P43
- P50
- P51
- P60
- P61
- P62
- P80
- P81
- P85
- P91

---

## 11. Sonuç
Bu belge, sistemin ajanlar arası konuşma, runtime, QA, governance ve release omurgasının kayıt defteri olarak korunur.
