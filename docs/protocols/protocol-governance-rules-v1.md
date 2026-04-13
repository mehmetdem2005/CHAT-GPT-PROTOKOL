# Protocol Governance Rules v1

Bu belge, protokollerin nasıl evrileceğini, kim tarafından değiştirileceğini ve ne zaman breaking change sayılacağını netleştirir.

## Amaç
- Protokol değişikliklerini rastgele belge düzenleme olmaktan çıkarmak
- Versioning, ownership, review ve rollout disiplinini tanımlamak
- Ayrı sohbetlerde gelişen modüller arasında contract kırılmasını önlemek

---

## 1. Protokol Değişiklik Sınıfları
### Class A — Editorial
Yalnız açıklama düzeltmesi, typo veya örnek iyileştirmesi.

### Class B — Additive Non-Breaking
- optional field ekleme
- yeni metadata alanı
- yeni örnek ekleme
- error detail genişletme

### Class C — Behavioral Clarification
- muğlak semantiği netleştirme
- lifecycle geçişlerini açıklama
- retry/idempotency davranışını kesinleştirme

### Class D — Breaking Contract Change
- required field ekleme
- required field silme
- field type değişikliği
- enum değeri kaldırma
- compatibility bozan lifecycle semantik değişikliği

---

## 2. Onay Kuralları
### Class A
- hafif review yeterli olabilir

### Class B
- protocol owner review
- fixture güncellemesi

### Class C
- protocol owner review
- etkilenen modül sahipleri gözden geçirmesi
- compatibility notu

### Class D
- explicit approval
- major version bump
- migration note
- backward compatibility plan veya sunset plan

---

## 3. Protocol Owner Modeli
Her protokol için en az şu roller tanımlanmalıdır:
- `protocolOwner`
- `reviewOwners`
- `fixtureOwner`
- `releaseApprover` gerekiyorsa

### Sorumluluklar
Protocol owner:
- şema ve semantik doğruluğu korur
- versiyon kararını verir
- breaking change açıklamasını yazar

Fixture owner:
- valid/invalid örnekleri günceller
- CI fixture validation’ı takip eder

Review owners:
- etkilenen ajan ve servislerde geriye uyumluluğu kontrol eder

---

## 4. Versioning Kuralları
### Patch
- editorial düzeltme
- non-semantic örnek iyileştirmesi

### Minor
- backward-compatible additive değişiklik
- optional alan ekleme
- yeni non-breaking metadata

### Major
- breaking change
- lifecycle veya enum semantiğinde uyumluluğu bozan değişiklik

### Kural
Major version bump olmadan breaking change merge edilmez.

---

## 5. Sunset ve Deprecation Kuralları
Bir alan veya davranış deprecated olacaksa:
- açık işaretlenmeli
- yerine gelecek alan belirtilmeli
- kaldırma sürümü veya zaman penceresi yazılmalı
- fixture ve örneklerde deprecation notu görünmeli

### Kural
Deprecated alanı sessizce kaldırmak yasaktır.

---

## 6. Required Compatibility Checks
Her anlamlı protokol değişikliğinde şu kontroller düşünülmelidir:
- builder/validator uyumu
- fixture uyumu
- agent I/O örnekleri uyumu
- error envelope uyumu
- observability alanları uyumu
- preview/governance/referrer id alanları uyumu

---

## 7. CI Kuralları
Protocol change içeren PR veya commit için minimum:
- schema validation
- fixture validation
- protocol-sdk typecheck
- backward compatibility smoke test (uygunsa)

### Kural
CI geçmeden protokol authoritative sayılmaz.

---

## 8. Breaking Change Notu Şablonu
Breaking change olduğunda şu alanlar yazılmalıdır:
- ne değişti
- neden değişti
- hangi protokoller etkilendi
- hangi ajanlar/servisler etkilendi
- migration nasıl yapılacak
- eski sürüm ne zaman sunset olacak

---

## 9. Cross-Conversation Development Kuralı
Ayrı sohbetlerde geliştirilen modüller için:
- konuşma içi varsayım değil protocol dokümanı esas alınır
- anlaşmazlık varsa implementation değil protocol netleştirilir
- aynı protokolün paralel iki yorumu authoritative olamaz

---

## 10. Minimum Governance Seti
Her çekirdek protokol için minimum governance beklentisi:
- owner belli
- version belli
- valid minimal fixture var
- invalid fixture var
- breaking rules yazılı
- change history takip edilebilir

---

## 11. Sonuç
Bu belge, protokol setinin zamanla büyürken dağılmamasını sağlayan resmi yönetişim kurallarını tanımlar.
