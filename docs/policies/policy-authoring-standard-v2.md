# Policy Authoring Standard v2

Bu belge, repo içindeki tüm politika ailelerinin ve alt politikaların yüksek kalite standardında nasıl yazılması gerektiğini tanımlar.

## 1. Her Politika İçin Zorunlu Alanlar
- policy id
- title
- objective
- business rationale
- scope
- non-scope
- actors and owners
- trigger conditions
- required inputs
- evidence sources
- decision logic
- enforcement mode
- severity model
- exception path
- escalation path
- audit requirements
- metrics
- review cadence
- change history

## 2. Policy Şablonu
### Policy Header
- Policy ID
- Family
- Version
- Status
- Owner
- Reviewers
- Approved By

### Intent
- Objective
- Why this policy exists
- Risks addressed

### Applicability
- In scope
- Out of scope
- Affected systems
- Affected roles

### Decision Logic
- Inputs
- Preconditions
- Evaluation rules
- Decision outputs
- Conflict priority band

### Enforcement
- advisory / warn / soft_block / approval_gate / hard_block / release_hold
- enforcing systems
- human review points

### Exceptions
- who can request exception
- who can approve exception
- evidence required
- expiry and re-review

### Evidence and Audit
- required records
- audit references
- logs / traces / metrics

### Failure Modes
- violation patterns
- user impact
- release impact
- recovery expectations

## 3. Politika Kalite Kriterleri
Bir politika kaliteli sayılmak için:
- aynı durumda iki farklı yorum üretmemeli
- enforcement sahibi belli olmalı
- severity bandı net olmalı
- release etkisi net olmalı
- evidence gereksinimi yazılı olmalı
- exception süreci tanımlı olmalı

## 4. Düşük Kalite Göstergeleri
- sadece slogan cümlesi
- owner yok
- exception path yok
- audit şartı yok
- decision output kümesi belirsiz
- trigger anı yazılmamış

## 5. Politika Ailesi ile Alt Politika İlişkisi
Her family belgesinde:
- aile amacı
- family-level risk modeli
- alt politika listesi
- primary subjects
- primary enforcement surface
olmalıdır.

Her alt politikada ise:
- tekil rule mantığı
- ölçülebilir pass criteria
- violation örnekleri
olmalıdır.

## 6. Sonuç
Bu standart, repodaki politika belgelerini yalnız teorik metin olmaktan çıkarıp enforcement-ready hale getirmek için kullanılır.
