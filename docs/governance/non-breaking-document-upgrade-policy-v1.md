# Non-Breaking Document Upgrade Policy v1

Bu belge, repo içindeki belge yükseltmelerinin rewrite değil controlled in-place update olarak yapılacağını tanımlar.

## 1. Temel Kural
Belgeler geliştirilecek, netleştirilecek ve sertleştirilecektir; ancak mümkün olduğunca mevcut kimlik, soy ağacı ve referans yapısı korunacaktır.

## 2. Yasak Yaklaşım
Aşağıdaki yaklaşım yasaktır:
- eski belgeyi silip tamamen yeni bir belge gibi yazmak
- mevcut policy veya protocol id’lerini sebepsiz değiştirmek
- lineage ve backward reference’ları kaybetmek
- eski yapıyı görünmez kılmak

## 3. Tercih Edilen Yaklaşım
Aşağıdaki yaklaşım zorunluya yakındır:
- in-place clarification
- additive structure
- metadata ekleme
- owner/reviewer/approver ekleme
- enforcement ve evidence bölümleri ekleme
- numbered procedure ekleme
- deprecation notice ile kontrollü evrim

## 4. Belge Güncelleme Sınıfları
- editorial update
- clarification update
- additive governance update
- compatibility-affecting update
- deprecation update

## 5. Non-Breaking Update Örnekleri
- açıklama ekleme
- exception path ekleme
- owner ve reviewer alanları ekleme
- examples ve evidence refs ekleme
- mandatory checks bölümü ekleme
- numbered operational procedure ekleme

## 6. Breaking Sayılabilecek Güncellemeler
- policy id değişikliği
- protocol id değişikliği
- mevcut lifecycle anlamını tersine çevirme
- eski sonucu yeni belgeyle sessizce geçersiz kılma
- compatibility notu olmadan required alan ekleme

## 7. Legacy Koruma Kuralı
Legacy lineage dosyaları ve önceki registry kayıtları korunacaktır.
Yeni belge seti, eski çekirdeği genişletir; onu silmez.

## 8. Sonuç
Bu politika, belge sisteminin kurumsal kaliteye yükselirken kimliğini ve tarihsel sürekliliğini bozmamasını sağlar.
