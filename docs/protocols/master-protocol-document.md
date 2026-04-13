# Master Protocol Document

Bu belge, farklı sohbetlerde geliştirilecek tüm bileşenlerin birbirleriyle uyumlu çalışmasını sağlamak için hazırlanmış ana sözleşmedir. Her sohbet başka bir bileşenin iç kodunu bilmese bile bu protokoller üzerinden sisteme entegre olabilir.

---

## 1. Sistem Amacı
Amaç, büyük bir uygulamayı bağımsız modüller halinde geliştirmek ve her modülün yalnızca tanımlı protokoller üzerinden haberleşmesini sağlamaktır.

Bu sistemde:
- Her modül bağımsız geliştirilebilir.
- Her modül diğer modüllerin iç implementasyonunu bilmek zorunda değildir.
- Entegrasyon ortak contract/protocol kuralları üzerinden yapılır.
- İç kod değişse bile dış contract bozulmadıkça sistem çalışmaya devam eder.

---

## 2. Temel Mimari İlkeler
### 2.1 Modülerlik
Her bileşen tek sorumluluğa sahip olmalıdır.

### 2.2 Contract-first geliştirme
Koddan önce interface, schema, event ve response kuralları tanımlanır.

### 2.3 Gevşek bağlılık
Bir modül başka bir modülün iç sınıflarına, fonksiyonlarına veya dosya yapısına bağımlı olamaz.

### 2.4 Sıkı doğrulama
Her giriş ve çıkış schema ile doğrulanmalıdır.

### 2.5 Geriye uyumluluk
Yeni sürümler mümkün olduğunca eski contract’ları bozmamalıdır.

### 2.6 Gözlemlenebilirlik
Her kritik işlem log, trace ve hata kodu ile izlenebilir olmalıdır.

---

## 3. Sistem Katmanları
Sistem aşağıdaki katmanlardan oluşur:
1. Client Layer
2. Gateway / API Layer
3. Application Services Layer
4. Domain Layer
5. Infrastructure Layer
6. Event / Messaging Layer

---

## 4. Zorunlu Protokol Kategorileri
Her modül aşağıdaki protokol alanlarına uymak zorundadır:
- kimlik
- sorumluluk sınırı
- interface contract
- veri contract’ı
- operasyon contract’ı

### 4.1 Kimlik
- `moduleId`
- `moduleName`
- `moduleVersion`
- `owner`

### 4.2 Sorumluluk sınırı
Her modül şunları açıklamalıdır:
- ne yapar
- ne yapmaz
- hangi girdileri kabul eder
- hangi çıktıları üretir
- hangi modüllere bağımlıdır
- hangi modüller ona bağımlıdır

### 4.3 Interface contract
- API endpoint’leri
- event isimleri
- command yapıları
- query yapıları
- response formatı
- error formatı

### 4.4 Veri contract’ı
- alan isimleri
- veri tipleri
- zorunlu / opsiyonel alanlar
- varsayılan değerler
- validation kuralları
- enum setleri

### 4.5 Operasyon contract’ı
- timeout
- retry politikası
- idempotency
- rate limit
- circuit breaker / fallback davranışı

---

## 5. İsimlendirme Standartları
- Teknik anahtarlar İngilizce yazılır.
- JSON alan adlarında `camelCase` kullanılır.
- Event isimleri `domain.entity.action.v1` formatını izler.
- API route’larında çoğul kaynak adı tercih edilir.
- Error code’lar büyük harf ve underscore ile yazılır.

---

## 6. Standart Request Envelope
```json
{
  "requestId": "req_123",
  "timestamp": "2026-04-12T10:00:00Z",
  "actor": {
    "type": "user",
    "id": "usr_123"
  },
  "context": {
    "sessionId": "ses_123",
    "traceId": "trc_123",
    "source": "web"
  },
  "payload": {}
}
```

---

## 7. Standart Response Envelope
```json
{
  "success": true,
  "requestId": "req_123",
  "traceId": "trc_123",
  "data": {},
  "meta": {
    "version": "1.0.0",
    "timestamp": "2026-04-12T10:00:01Z"
  },
  "error": null
}
```

Kurallar:
- `success=true` ise `error=null` olmalıdır.
- `success=false` ise `error` dolu olmalıdır.
- `requestId` ve `traceId` mümkünse her zaman dönmelidir.

---

## 8. Standart Error Formatı
```json
{
  "success": false,
  "requestId": "req_123",
  "traceId": "trc_123",
  "data": null,
  "meta": {
    "version": "1.0.0",
    "timestamp": "2026-04-12T10:00:01Z"
  },
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Payload validation failed.",
    "details": [
      {
        "field": "email",
        "reason": "invalid_format"
      }
    ],
    "retryable": false
  }
}
```

Tavsiye edilen ortak hata kodları:
- `VALIDATION_ERROR`
- `UNAUTHORIZED`
- `FORBIDDEN`
- `RESOURCE_NOT_FOUND`
- `CONFLICT`
- `RATE_LIMIT_EXCEEDED`
- `DEPENDENCY_FAILURE`
- `TIMEOUT`
- `INTERNAL_ERROR`
- `NOT_IMPLEMENTED`

---

## 9. Event Protocol Standardı
```json
{
  "eventId": "evt_123",
  "eventName": "billing.invoice.created.v1",
  "eventVersion": "1",
  "occurredAt": "2026-04-12T10:00:00Z",
  "producer": "billing-service",
  "traceId": "trc_123",
  "idempotencyKey": "idem_123",
  "payload": {}
}
```

Kurallar:
- Event immutable kabul edilir.
- Event tüketicileri idempotent olmak zorundadır.
- Event sürümü kırıcı değişiklikte artırılmalıdır.

---

## 10. Versioning Kuralı
Semantic Versioning kullanılacaktır:
- `MAJOR`: kırıcı değişiklik
- `MINOR`: geriye uyumlu yeni özellik
- `PATCH`: hata düzeltmesi

Contract versioning kuralları:
- alan silmek kırıcı değişikliktir
- alan adını değiştirmek kırıcı değişikliktir
- enum’dan değer silmek kırıcı değişikliktir
- yeni opsiyonel alan eklemek geriye uyumludur

---

## 11. Güvenlik Protokolleri
- input validation
- output filtering
- authentication
- authorization
- secret handling
- auditability

---

## 12. Gözlemlenebilirlik Protokolleri
Her modül şu sinyalleri üretebilmelidir:
- structured logs
- metrics
- traces
- health checks

Zorunlu log alanları:
- `timestamp`
- `level`
- `module`
- `message`
- `traceId`
- `requestId`
- `actorId` (varsa)

Önerilen health endpoint’leri:
- `/health/live`
- `/health/ready`

---

## 13. Dayanıklılık Kuralları
- timeout
- retry
- idempotency
- fallback
- graceful degradation

---

## 14. Veri Sözleşmesi Kuralları
Her veri modeli için ayrı ayrı yazılmalıdır:
- entity tanımı
- field listesi
- tipler
- nullability
- validation
- lifecycle state’leri
- ilişkiler

---

## 15. Modül Şablonu
Her yeni sohbet bir modülü geliştirirken şu başlıkları doldurmalıdır:
- modül kimliği
- amaç
- sınırlar
- inputs
- outputs
- dependencies
- schemas
- operational rules
- security rules
- tests

---

## 16. Sohbetler Arası Geliştirme Kuralı
1. Sohbet sadece kendisine verilen modülü geliştirir.
2. Başka modüllerin gerçek kodunu varsaymaz.
3. Başka modülleri yalnızca bu belgede tanımlanan contract üzerinden görür.
4. Gerekirse mock interface kullanır.
5. Kod üretmeden önce ilgili modül contract’ını yazar veya günceller.
6. Üretilen kod contract’a uymuyorsa contract esas alınır.

---

## 17. Entegrasyon Kuralı
Bir modül tamamlandığında entegrasyon için minimum gereklilikler:
- contract dokümanı tamamlanmış olmalı
- request/response örnekleri bulunmalı
- event örnekleri bulunmalı
- error örnekleri bulunmalı
- mock testleri geçmeli
- contract testleri geçmeli

---

## 18. Karar Hiyerarşisi
Çakışma olduğunda şu sıra geçerlidir:
1. Master Protocol Document
2. Domain-specific protocol
3. Module contract
4. Implementation detail

Yani kod, sözleşmeyi geçersiz kılamaz.

---

## 19. Başlangıçta Oluşturulacak Ana Belgeler
1. Master Protocol Document
2. System Module Registry
3. Global Error Code Registry
4. Event Catalog
5. API Style Guide
6. Security Policy
7. Observability Standard
8. Testing Standard
9. Deployment and Environment Contract
10. Per-module contract files

---

## 20. Sonuç
Bu belge, sistemin contract-first, protocol-driven ve ayrı sohbetlerde güvenle geliştirilebilir çekirdek omurgasının ana anayasa belgesidir.
