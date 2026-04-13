# Full Document System Upgrade Charter v1

Bu belge, repo içindeki yükseltme kapsamının yalnız politika aileleriyle sınırlı olmadığını resmi olarak tanımlar.

## 1. Amaç
Kapsamı açıkça sabitlemek:
- policies
- protocols
- procedures
- runbooks
- standards
- registries
- schemas
- governance notes
- checklists
- incident and release records için yazım şablonları

## 2. Temel İlke
Kapsam **33 politika ailesi** ile sınırlı değildir.
33 aile yalnız policy family katmanıdır.
Asıl yükseltme kapsamı, repodaki tüm belge sistemidir.

## 3. Dahil Olan Belge Sınıfları
### Policy katmanı
- policy registry
- policy family belgeleri
- policy authoring standards
- legacy lineage belgeleri

### Protocol katmanı
- master protocol document
- protocol registry
- protocol clarifications
- protocol governance rules
- protocol gap analysis
- proposed new protocols
- protocol-specific schemas ve specs

### Procedure / Runbook katmanı
- incident runbooks
- rollback / approval / release procedures
- preview operations procedures
- deployment procedures
- change management procedures

### Standard katmanı
- document authoring standards
- policy authoring standards
- protocol governance standards
- quality gates

### Registry / Schema katmanı
- turn state
- artifact manifest
- diagnostics taxonomies
- mapping belgeleri

## 4. Hedef
Repo, dağınık belge koleksiyonu değil, kurumsal olarak işletilebilir bir belge sistemi olmalıdır.

## 5. Başarı Tanımı
Yükseltme başarılı sayılmak için:
- her kritik belge owner taşır
- reviewer ve approver zinciri görünür olur
- mandatory checks yazılı olur
- exception path yazılı olur
- evidence refs tanımlanır
- numbered procedures kullanılır
- deprecation ve migration kuralları bulunur
- release ve incident bağları netleşir
- non-breaking update ilkesi korunur

## 6. Sonuç
Bu charter, belge yükseltme programının yalnız 33 aileyi değil, tüm belge sistemini kapsadığını resmi hale getirir.
