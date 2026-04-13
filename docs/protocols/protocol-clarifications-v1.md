# Protocol Clarifications v1

Bu belge, mevcut protokol setindeki muğlak noktaları netleştirmek için hazırlanmıştır.

## Amaç
- Protokoller arası yorum farkını azaltmak
- Ayrı sohbetlerde geliştirilen bileşenlerin aynı anlam modelini kullanmasını sağlamak
- Zorunlu alan, lifecycle, readiness, idempotency ve compatibility kurallarını kesinleştirmek

---

## 1. Kimlik Hiyerarşisi
Aşağıdaki kimlikler birbirinin yerine kullanılmaz:

- `workspaceId`: ürün/stüdyo çalışma alanı
- `sessionId`: bir workspace içindeki çalışma oturumu
- `turnId`: çok turlu akış içindeki tek tur
- `graphId`: ilgili tur için üretilen görev grafı
- `taskId`: tekil ajan görevi
- `manifestId`: artifact kayıt seti
- `previewSessionId`: preview çalışma oturumu
- `buildId`: build çalıştırması
- `runtimeId`: çalışan preview runtime örneği
- `approvalId`: approval kaydı
- `rollbackId`: rollback planı veya uygulaması
- `traceId`: gözlemlenebilirlik korelasyonu

### Kural
- `traceId` iş kimliği değildir.
- `turnId` task veya preview kimliği değildir.
- `manifestId` snapshot yerine kullanılamaz.

---

## 2. Zorunlu Korelasyon Alanları
Aşağıdaki protokol sınıflarında korelasyon alanları zorunlu kabul edilir:

### Task ve graph protokolleri
- `turnId`
- `traceId`
- `taskId` veya `graphId`

### Preview protokolleri
- `turnId`
- `traceId`
- `previewSessionId`

### Governance protokolleri
- `turnId`
- `traceId`
- ilgili `approvalId` / `rollbackId` / `interventionId`

### Kural
Bir protokol kritik akışa aitse ve `traceId` taşımıyorsa eksik sayılır.

---

## 3. Required ve Optional Alan Semantiği
### Required
- alan payload’da bulunmalıdır
- `null` ile gönderilmesi allowed değilse ayrıca belirtilmelidir
- validation failure doğurur

### Optional
- alan yok olabilir
- varsa tip ve içerik kurallarına uymalıdır
- optional alanın varlığı davranışı değiştirebilir ama temel sözleşmenin yerine geçmez

### Nullable
- alan bulunur ama değeri `null` olabilir
- optional ile aynı şey değildir

### Kural
Yeni sürümde required alan eklemek breaking change kabul edilir.

---

## 4. Status Alanları için Ortak Semantik
Aşağıdaki durum isimleri tüm protokollerde mümkün olduğunca aynı anlamı taşımalıdır:

- `pending`: henüz işlenmedi
- `accepted`: sistem işi sahiplenmiş ama çalıştırmamış olabilir
- `running`: aktif yürütülüyor
- `blocked`: ilerleme dış koşul nedeniyle durdu
- `awaiting_input`: kullanıcı girdisi bekleniyor
- `awaiting_approval`: açık onay bekleniyor
- `completed`: başarıyla bitti
- `failed`: başarısız kapandı
- `rolled_back`: önceki güvenli duruma geri döndü

### Kural
`blocked` ile `failed` karıştırılamaz.
- `blocked` çözülebilir bekleme durumudur
- `failed` mevcut denemenin başarısız kapandığını söyler

---

## 5. Turn State Geçiş Kuralları
Geçerli örnek akış:
- `open`
- `awaiting_user_input`
- `open`
- `awaiting_approval`
- `completed`

Alternatif akışlar:
- `open -> awaiting_fix -> completed`
- `open -> failed`
- `open -> rolled_back`

### Yasak geçiş örnekleri
- `failed -> completed` doğrudan
- `rolled_back -> completed` doğrudan
- `awaiting_approval -> awaiting_user_input` gerekçesiz

### Kural
Geçişler reason veya event ref ile desteklenmelidir.

---

## 6. Task Contract Clarifications
Bir task contract şunları açıkça taşımalıdır:
- görevin amacı
- sınırları
- bağımlılıkları
- beklenen output tipleri
- timeout davranışı
- retry güvenliği
- approval ipuçları

### Netleştirme
- `expectedOutputs` boşsa görev gözlem veya doğrulama görevi olabilir
- `constraints` boş bırakılabilir ama yorum gerektiren gizli constraint kabul edilmez
- `inputRefs` ile `inlineInput` aynı anda olabilir; çelişirse `inlineInput` yalnız açık override olarak kullanılmalıdır

---

## 7. Idempotency Kuralları
Aşağıdaki işlemler idempotency düşünmelidir:
- event publish
- task dispatch
- build trigger
- preview rerun
- approval resolve
- rollback execute

### Kural
Aynı `idempotencyKey` ile gelen tekrar istekler:
- ikinci kez yıkıcı yan etki üretmemelidir
- mümkünse ilk sonucu referans olarak döndürmelidir

### Not
Her istek idempotent olmak zorunda değildir; ama yıkıcı veya tekrar tetiklenebilir kritik aksiyonlar için zorunluya yakındır.

---

## 8. Retry Kuralları
Retry yalnız şu koşullarda güvenli kabul edilir:
- aynı iş tekrarlandığında veri bozulmuyor
- duplicate artifact oluşmuyor
- duplicate approval veya rollback kararı doğmuyor
- side effect kontrollü

### Retry yapılmaması gereken tipik durumlar
- approval resolve
- rollback execute
- lock mutation
- tenant boundary sensitive write

### Kural
Retry policy protokol dışı saklanamaz; task veya operation contract’ında görünmelidir.

---

## 9. Event İmmutability Kuralları
Event’ler immutable kabul edilir.

### Bu ne anlama gelir?
- event yayınlandıktan sonra payload değiştirilmez
- düzeltme gerekiyorsa yeni event yayınlanır
- event replay olasılığı düşünülür

### Kural
Event consumer’lar duplicate consume durumunda idempotent davranmalıdır.

---

## 10. Versioning Clarifications
### Breaking değişiklik örnekleri
- required field eklemek
- field silmek
- field type değiştirmek
- enum değeri kaldırmak
- status semantiğini değiştirmek

### Non-breaking değişiklik örnekleri
- optional field eklemek
- yeni metadata eklemek
- yeni warning alanı eklemek

### Kural
Bir protokol sürümü yükseltilmeden breaking değişiklik yapılmaz.

---

## 11. Preview Readiness Anlamı
### `ready`
- build tamamlandı
- runtime ayağa kalktı
- en az bir kritik route doğrulandı
- panel senkronizasyonu kuruldu

### `partially_ready`
- preview gözlenebilir ama tüm kritik yüzeyler hazır değil

### `degraded`
- preview kullanılabilir ama ciddi sınırlamalar veya warning’ler var

### `failed`
- build veya runtime veya kritik route eşiği geçilemedi

### Kural
`ready` olmak release-ready olmak anlamına gelmez.

---

## 12. Manifest Clarifications
Manifest şu sorulara cevap verebilmelidir:
- hangi artifact var
- kim üretti
- neden üretildi
- hangi contract’ı etkiliyor
- hangi preview route’larını etkiliyor
- rollback için hangi snapshot’lar var

### Kural
Manifest’te görünmeyen kritik artifact sistemde görünür gerçeklik kabul edilmemelidir.

---

## 13. Lock Clarifications
Lock türleri farklı otorite seviyeleri taşır:
- `user_lock`
- `operator_lock`
- `policy_lock`
- `approval_lock`
- `release_lock`

### Öncelik
`policy_lock` ve `approval_lock`, sıradan heuristik önerilerden üstündür.

### Kural
Lock’lar sessiz şekilde overwrite edilemez; unlock veya override olayı görünür olmalıdır.

---

## 14. Approval Clarifications
Bir approval kaydı şu soruları cevaplamalıdır:
- ne onaylanıyor
- neden onay gerekiyor
- onay gelmezse ne olur
- hangi scope etkileniyor
- reddedilirse hangi graph veya task supersede olur

### Kural
`approval_pending`, pratikte `allow` değildir.

---

## 15. Rollback Clarifications
Rollback, regeneration ile aynı şey değildir.

### Regeneration
- yeniden üretir
- mevcut state’i tamamen geri almaz

### Rollback
- önceki güvenli noktaya döner
- manifest ve snapshot eşleşmesi bekler
- governance ve audit etkisi taşır

### Kural
Safe point olmadan rollback planı zayıf kabul edilmelidir.

---

## 16. Error Alanı Netleştirmesi
Error envelope içinde:
- `code` makine tarafından işlenebilir olmalı
- `message` insan tarafından okunabilir olmalı
- `retryable` operasyonel davranışı etkilemeli
- `details` tanı için yardımcı olmalı ama secret içermemeli

### Kural
Teknik detay ile kullanıcı mesajı aynı alan içine yığılmamalıdır.

---

## 17. Protocol Ownership Kuralı
Her protokol için sahibi net olmalıdır:
- kim sürüm yükseltir
- kim breaking change onaylar
- kim fixture’ları günceller
- kim geriye uyumluluğu doğrular

### Kural
Sahibi belli olmayan protokol üretimde authoritative kabul edilmemelidir.

---

## 18. Fixture Zorunluluğu
Çekirdek protokoller için en az şu fixture türleri olmalıdır:
- valid minimal payload
- valid full payload
- invalid missing required field
- invalid enum
- backward compatibility sample

### Kural
Fixture’sız protokol yalnız metin belgesi olarak kalır; entegrasyon güveni düşüktür.

---

## 19. Compatibility Kuralı
Ayrı sohbetlerde geliştirilen modüller için resmi kural:
- iç implementasyon bilinmeyebilir
- ama protocol shape, version ve error davranışı bilinmelidir
- yorum boşluğu varsa implementation değil protocol düzeltilir

---

## 20. Sonuç
Bu belge, mevcut protokol setinin yorum farkı yaratabilecek alanlarını sıkılaştırır ve contract-first geliştirmeyi daha güvenli hale getirir.
