# Policy Extension Control Pack v1

Bu belge, mevcut 33 policy family yapısını bozmadan eksik kalan yüksek değerli policy kontrollerini ekler.

## Amaç
- mevcut family yapısını genişletmek
- operasyonel boşlukları doldurmak
- procedure ve release zincirine güçlü bağ kurmak

---

## PX-001 — Policy Exception Expiry Policy
**Maps To:** PL-013, PL-032
**Rule:** Açılan her policy exception süreli olmalı ve expiry olmadan kalıcı hale gelmemelidir.
**Enforcement:** require_review / hard_block on expired exception

## PX-002 — Waiver Evidence Policy
**Maps To:** PL-011, PL-013
**Rule:** QA veya release waiver kararı evidence refs ve approver zinciri olmadan geçerli sayılmaz.
**Enforcement:** release_hold

## PX-003 — Feature Flag Ownership Policy
**Maps To:** PL-014, PL-032
**Rule:** Her feature flag owner, expiry ve cleanup planı taşımalıdır.
**Enforcement:** require_review

## PX-004 — Configuration Drift Visibility Policy
**Maps To:** PL-010, PL-032
**Rule:** Kritik config değişiklikleri drift üretiyorsa görünür kayıt ve review gerektirir.
**Enforcement:** require_review / release_hold

## PX-005 — Vendor Fallback Policy
**Maps To:** PL-020
**Rule:** Kritik vendor entegrasyonlarında failure behavior veya fallback planı bulunmalıdır.
**Enforcement:** require_review / hard_block for critical path

## PX-006 — Tenant Evidence Policy
**Maps To:** PL-030, PL-031
**Rule:** Tenant isolation iddiaları teknik evidence refs olmadan yeterli kabul edilmez.
**Enforcement:** hard_block

## PX-007 — Secret Rotation Readiness Policy
**Maps To:** PL-006
**Rule:** Kritik secret sınıfları rotation-ready tanımlanmalı ve sızıntı sonrası response yolu olmalıdır.
**Enforcement:** require_review / hard_block

## PX-008 — Incident Communications Policy
**Maps To:** PL-021, PL-023
**Rule:** Kritik incident’lerde internal ve gerekirse user-facing communication yolu tanımlı olmalıdır.
**Enforcement:** require_review

## PX-009 — Preview Failure Disclosure Policy
**Maps To:** PL-010, PL-011
**Rule:** Preview başarısızlığı kullanıcı yüzeyinde sessizce gizlenmemeli; anlaşılır durum etiketi gösterilmelidir.
**Enforcement:** require_review

## PX-010 — Rollback Validation Policy
**Maps To:** PL-013, PL-022
**Rule:** Rollback tamamlandı sayılmadan önce validation sonucu kaydedilmelidir.
**Enforcement:** require_review / release_hold

## PX-011 — Protocol Deprecation Notice Policy
**Maps To:** PL-009, PL-018, PL-032
**Rule:** Deprecated protocol veya alan replacement ve sunset bilgisi olmadan sessizce kaldırılamaz.
**Enforcement:** hard_block

## PX-012 — Documentation Currency Policy
**Maps To:** PL-018
**Rule:** Kritik protocol, policy ve procedure değişikliklerinde docs drift belirli eşik üstüne çıkamaz.
**Enforcement:** require_review / release_hold

## PX-013 — Approval Independence Policy
**Maps To:** PL-013
**Rule:** Approval-bound kritik kararlarda self-approval varsayılan olarak yasak kabul edilir.
**Enforcement:** hard_block unless explicitly allowed

## PX-014 — Unsafe Output Escalation Policy
**Maps To:** PL-029, PL-021
**Rule:** Tekrarlayan unsafe output bulguları incident veya governance escalation üretebilmelidir.
**Enforcement:** require_review / hard_block

## PX-015 — Migration Note Required Policy
**Maps To:** PL-009, PL-032
**Rule:** Compatibility-affecting change migration note olmadan tamamlanmış sayılmaz.
**Enforcement:** require_review / release_hold
