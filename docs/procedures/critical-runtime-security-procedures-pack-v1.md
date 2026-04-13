# Critical Runtime & Security Procedures Pack v1

Bu belge, preview, runtime, tenant isolation, security ve recovery alanlarında eksik kalan kritik prosedürleri toplar.

## RP-01 — Preview Failure Triage Procedure
**Trigger:** preview failed, degraded veya unstable.
**Steps:**
1. Failure domain belirle: build, startup, route, render, panel.
2. Last successful state’i bul.
3. Affected routes ve viewports’u listele.
4. Rerun, safe mode veya fix path seç.
5. Turn state ve diagnostics refs güncelle.
**Completion:** triage_complete.

## RP-02 — Build Failure Triage Procedure
**Trigger:** build_failed.
**Steps:**
1. Failure category ata.
2. Log ve artifact refs topla.
3. Dependency, syntax, type veya config kökünü ayır.
4. Minimal fix owner’ı ata.
5. Retry koşulu güvenliyse rerun planı oluştur.
**Completion:** build_fix_requested veya rerun_authorized.

## RP-03 — Rollback Execution Procedure
**Trigger:** approved rollback veya critical regression.
**Steps:**
1. Target snapshot doğrula.
2. Scope ve affected artifacts listesini sabitle.
3. Approval zorunluluğunu kontrol et.
4. Manifest ve turn refs güncelle.
5. Post-rollback preview veya validation başlat.
**Completion:** rollback_executed veya rollback_failed.

## RP-04 — Rollback Validation Procedure
**Trigger:** rollback tamamlandı.
**Steps:**
1. Artifact integrity kontrol et.
2. Route availability ve preview durumunu ölç.
3. Temel QA smoke sonuçlarını topla.
4. Release gate etkisini yeniden değerlendir.
5. Validation outcome kaydı üret.
**Completion:** rollback_validated veya rollback_needs_review.

## RP-05 — Runtime Health Escalation Procedure
**Trigger:** repeated degraded/unready/unstable health.
**Steps:**
1. Health signal ve trend refs topla.
2. Incident açılması gerekip gerekmediğini değerlendir.
3. Owner ve operator’ı haberdar et.
4. Freeze, reroute veya safe mode kararı ver.
5. Audit ve incident linklerini oluştur.
**Completion:** escalated veya contained.

## RP-06 — Tenant Isolation Verification Procedure
**Trigger:** auth, storage, cache, preview veya topology değişikliği.
**Steps:**
1. Tenant scope boundaries listele.
2. Cross-tenant read/write risklerini test et.
3. Cache, preview ve namespace ayrımını doğrula.
4. Blocking finding varsa release hold üret.
5. Evidence bundle kaydet.
**Completion:** isolation_verified veya isolation_blocked.

## RP-07 — Secret Exposure Response Procedure
**Trigger:** secret leak, credential exposure veya config sızıntısı şüphesi.
**Steps:**
1. Etkilenen secret class’ı tanımla.
2. Maruz kalan yüzeyleri izole et.
3. Rotation ihtiyacını belirle.
4. Incident ve audit kayıtlarını aç.
5. Sonraki doğrulama adımlarını ata.
**Completion:** contained veya escalated.

## RP-08 — Security Review Procedure
**Trigger:** auth, admin, payment, export, automation veya integration değişikliği.
**Steps:**
1. Review scope belirle.
2. Relevant policy ve protocol refs topla.
3. Findings ve severity summary üret.
4. Required fixes veya waiver ihtiyacını işaretle.
5. Release impact kararı ver.
**Completion:** review_passed, review_failed veya waiver_required.

## RP-09 — Privacy Review Procedure
**Trigger:** yeni veri alanı, analytics genişlemesi veya export/sync akışı.
**Steps:**
1. Data classes ve retention refs topla.
2. Minimization ve default behavior kontrol et.
3. Deletion/correction etkisini doğrula.
4. Compliance mapping etkisini işaretle.
5. Review kararını kaydet.
**Completion:** privacy_passed veya privacy_blocked.

## RP-10 — Vendor Security Review Procedure
**Trigger:** yeni üçüncü taraf entegrasyon veya vendor değişimi.
**Steps:**
1. Vendor scope ve data boundary belirle.
2. Auth mode ve failure modelini değerlendir.
3. SLA ve fallback yeterliliğini incele.
4. Approval gereksinimini işaretle.
5. Risk notes ve decision kaydı üret.
**Completion:** vendor_approved, vendor_restricted veya vendor_blocked.
