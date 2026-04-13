# Legacy Protocol Lineage

Bu belge, önceki protokol omurgasının unutulmaması için eklenmiştir.

## Amaç
- İlk PDF içindeki çekirdek protokol belgelerini repo içinde korumak
- Yeni mimari belgeler ile eski protocol-first omurga arasındaki sürekliliği görünür kılmak
- Ayrı sohbetlerde geliştirilecek modüller için ortak tarihsel referans bırakmak

## Legacy Core Protocol Set
Korunan erken omurga şu belgelerden oluşur:
1. Master Protocol Document
2. Protocol Registry v1
3. Turn State Schema v1
4. Artifact Manifest Schema v1
5. Preview Runtime Protocol Spec v1
6. Intervention & Rollback Spec v1

## Legacy Global Kurallar
Bu ilk omurgadan gelen ve korunması gereken çekirdek ilkeler:
- contract-first geliştirme
- gevşek bağlılık
- sıkı schema doğrulama
- request/response/event envelope standardı
- versioned contracts
- audit ve traceability
- timeout, retry, idempotency ve fallback disiplinleri
- ayrı sohbetlerde yalnız contract üzerinden entegrasyon

## Yeni Belgelerle İlişki
Legacy protokol omurgası yeni belgeler tarafından silinmez, genişletilir.

### Örnek bağlar
- Master Protocol Document -> sistem anayasası ve çalışma ilkeleri
- Protocol Registry v1 -> daha sonra ayrıntılandırılan protocol-sdk ve mapping belgelerinin kökü
- Turn State Schema v1 -> turn orchestration ve decision memory omurgasının kökü
- Artifact Manifest Schema v1 -> patch, ownership, QA ve rollback izlenebilirliğinin kökü
- Preview Runtime Protocol Spec v1 -> preview diagnostics, CI/CD ve deployment topolojisinin öncülü
- Intervention & Rollback Spec v1 -> conflict resolution, approval, governance ve incident recovery omurgasının öncülü

## Sonuç
Repo içindeki yeni mimari ve operasyon belgeleri, legacy protokol omurgasının üstüne inşa edilir. Bu soy ağacı korunmalıdır.
