# Critical Governance Procedures Pack v1

Bu belge, policy ve protocol omurgasını fiilen işletmek için gereken kritik governance prosedürlerini toplar.

## GP-01 — Policy Exception Procedure
**Trigger:** Bir kural geçici olarak aşılamadan ilerlenemiyor.
**Prerequisites:** ilgili policy ref, risk summary, owner bilgisi.
**Steps:**
1. İstisna talebini aç.
2. Etkilenen subject ve scope’u yaz.
3. Risk ve gerekçeyi belgeye bağla.
4. Gerekli approver zincirini belirle.
5. Expiry ve review tarihini koy.
6. Kararı audit kaydına bağla.
**Evidence:** exception request, approval ref, expiry date.
**Completion:** allow_with_exception veya denied.

## GP-02 — Approval Request Procedure
**Trigger:** approval-bound change, riskli release veya major structural karar.
**Steps:**
1. Approval subject’i tanımla.
2. Evidence refs ekle.
3. Required approvers listesini çöz.
4. Blocking etkileri görünür yap.
5. Approval kaydını publish et.
**Completion:** pending state oluşur.

## GP-03 — Approval Resolution Procedure
**Trigger:** approval request yanıtlandı.
**Steps:**
1. Approver kimliğini doğrula.
2. Self-approval yasağını kontrol et.
3. Approved veya rejected durumunu kaydet.
4. Decision log ve audit kaydını güncelle.
5. Turn state ve release gate etkisini uygula.
**Completion:** approved, rejected veya expired.

## GP-04 — Change Request Procedure
**Trigger:** schema, config, protocol, module boundary veya critical patch değişikliği.
**Steps:**
1. Change type’ı belirle.
2. Impact summary oluştur.
3. Target refs ekle.
4. Rollback veya mitigation yolunu yaz.
5. Review ve approval ihtiyacını işaretle.
**Completion:** accepted_for_review veya rejected.

## GP-05 — Protocol Change Procedure
**Trigger:** protocol field, lifecycle veya semantic update isteği.
**Steps:**
1. Change class belirle.
2. Breaking olup olmadığını değerlendir.
3. Fixture etkisini işaretle.
4. Owner ve reviewers onayını iste.
5. Deprecation veya migration notu gerekiyorsa ekle.
**Completion:** merged veya deferred.

## GP-06 — Protocol Deprecation Procedure
**Trigger:** protocol, field veya davranış emekliye ayrılıyor.
**Steps:**
1. Deprecated subject’i tanımla.
2. Replacement ref ekle.
3. Sunset version belirle.
4. Migration note yaz.
5. Registry ve fixtures’ı işaretle.
**Completion:** deprecated_notice_published.

## GP-07 — Release Approval Procedure
**Trigger:** release candidate oluşturuldu.
**Steps:**
1. Preview, QA, policy ve risk refs topla.
2. Blocking issue kalmadığını kontrol et.
3. Approval zincirini çalıştır.
4. Release decision kaydı üret.
5. Rollout veya hold kararı ver.
**Completion:** allow, defer veya block.

## GP-08 — Release Freeze Procedure
**Trigger:** incident, critical risk veya governance hold.
**Steps:**
1. Freeze reason kaydet.
2. Etkilenen release scope’u tanımla.
3. Deployment ve pipeline sahiplerini bilgilendir.
4. Unfreeze şartlarını yaz.
5. Audit ve status kaydını güncelle.
**Completion:** freeze_active.

## GP-09 — Hotfix Procedure
**Trigger:** production veya preview kritik kusuru acil düzeltme gerektiriyor.
**Steps:**
1. Hotfix subject’i ve kapsamı tanımla.
2. Normal akıştan sapma gerekçesini yaz.
3. Minimal change hedefi belirle.
4. Gerekli hızlı review zincirini çalıştır.
5. Sonradan tam review takibini aç.
**Completion:** hotfix_released veya hotfix_rejected.

## GP-10 — Incident Declaration Procedure
**Trigger:** P1-P4 sınıfına girebilecek operasyonel bozulma.
**Steps:**
1. Incident kaydı aç.
2. Severity ata.
3. Owner ve comms sorumlusunu ata.
4. Etkilenen scope’u yaz.
5. Containment aksiyonlarını başlat.
**Completion:** incident_open.

## GP-11 — Postmortem Procedure
**Trigger:** P1/P2 veya önemli tekrar eden olay.
**Steps:**
1. Timeline oluştur.
2. Root cause class yaz.
3. Contributing factors ekle.
4. Corrective actions ata.
5. Sahiplik ve tarihleri bağla.
**Completion:** postmortem_published.

## GP-12 — RCA Closure Procedure
**Trigger:** corrective action’lar tamamlandı.
**Steps:**
1. Action item durumlarını doğrula.
2. Kalıcı düzeltme evidence’ını ekle.
3. Riskin düştüğünü göster.
4. Problem kaydını kapat veya açık bırak.
**Completion:** rca_closed veya followup_required.
