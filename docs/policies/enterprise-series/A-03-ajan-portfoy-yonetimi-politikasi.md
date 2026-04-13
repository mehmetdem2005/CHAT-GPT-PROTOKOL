[Ajan Portföy Yönetimi Politikası]

1. AMAÇ: 60 ajanlı üretim uygulamasında tüm ajan ailelerinin yaşam döngüsünün, portföy kayıtlarında eksiksiz izlenmesini ve düşük değerli ya da yinelenen ajanların 90 gün içinde kapatılmasını garanti etmektir.

2. KAPSAM:
   - Hangi ajan tipleri?
     - Veri toplayıcı ajanlar
     - Analiz ve sınıflandırma ajanları
     - Karar ajanları
     - Planlama ve orkestrasyon ajanları
     - Eylem ajanları
     - Doğrulama, denetim ve geri besleme ajanları
     - Yardımcı ve sistem ajanları
   - Hangi ortamlar?
     - Geliştirme
     - Test
     - Staging
     - Üretim
   - Hangi sistem bileşenleri?
     - Ajan kayıt defteri
     - Portföy yönetim sistemi
     - Orkestrasyon katmanı
     - Kimlik ve yetki katmanı
     - Mesaj kuyruğu
     - CI/CD hattı
     - Gözlemlenebilirlik platformu
     - Görev ve maliyet raporlama katmanı
   - Hangi zaman dilimleri?
     - Üretim ortamında 7/24
     - Portföy kaydı doğrulama kontrolleri 7/24
     - Haftalık portföy taraması her 7 günde 1 kez
     - Çeyreklik portföy gözden geçirmesi her 90 günde 1 kez
     - Yıllık stratejik portföy temizliği her 365 günde 1 kez

3. KURALLAR:
   - MUST: Her ajan ailesi, canlıya alınmadan önce portföy sisteminde benzersiz `portfolioId`, iş hedefi, owner rolü, yaşam döngüsü durumu, kritik seviye, maliyet sınıfı ve kapanış metriği ile kayıtlı olmalıdır; bu alanlardan herhangi biri eksikse dağıtım hattı 60 saniye içinde reddedilmelidir. (Otomatik: portföy kayıt şeması ve CI/CD validasyon loglarından kontrol edilir.)
   - SHALL: Üretim ortamında aktif ajan ailesi sayısı 60 temel aile + en fazla 15 geçici aile sınırını aşamaz; bu eşik aşıldığında yeni ajan kaydı 1 saniye içinde engellenmeli ve 24 saat içinde portföy daraltma incelemesi açılmalıdır. (Otomatik: portföy yönetim sistemi ve orkestrasyon kayıtlarından kontrol edilir.)
   - MUST: Her ajan ailesi için haftada en az 1 kez kullanım sıklığı, görev başarısı, maliyet sapması ve hata oranı içeren portföy sağlık puanı hesaplanmalıdır; 100 üzerinden 55 puanın altında kalan ajan aileleri 5 iş günü içinde portföy incelemesine alınmalıdır. (Otomatik: görev, hata ve maliyet metriklerinden kontrol edilir.)
   - SHALL: Aynı iş hedefi, aynı giriş tipi ve aynı çıkış tipine sahip iki ajan ailesi tespit edildiğinde, görev hacmi son 30 günde en az 500 ise yinelenen aileler için 10 iş günü içinde birleştirme veya kapatma kararı verilmelidir. (Otomatik: ajan katalog eşleme raporu ve portföy karşılaştırma çıktılarından kontrol edilir.)
   - MUST: Son 30 günde toplam görev sayısı 100’ün altında ve başarı oranı %85’in altında kalan ajan aileleri "zayıf aday" olarak etiketlenmeli; aynı durum 60 gün daha sürerse ilgili aile 90 gün içinde kapatma planına alınmalıdır. (Otomatik: görev yürütme logları ve portföy etiketleme kayıtlarından kontrol edilir.)
   - SHALL: Son 45 günde hiç görev almayan üretim ajan aileleri, 7 gün içinde "pasif" durumuna geçirilmeli; 90 gün boyunca pasif kalan ailelerin kimlikleri iptal edilmeli ve görev kabulü kalıcı olarak kapatılmalıdır. (Otomatik: görev zaman damgaları, kimlik sistemi ve portföy yaşam döngüsü kayıtlarından kontrol edilir.)
   - MUST: Her yeni ajan ailesi için canlıya geçmeden önce en az 1 giriş örneği, 1 çıkış örneği, 1 hata örneği ve 1 geri alma/iptal davranışı portföy kaydına bağlanmalıdır; eksik örnek sayısı 1 bile olsa staging üstü ortamlara dağıtım engellenmelidir. (Otomatik: ajan kayıt şeması ve artifact referanslarından kontrol edilir.)
   - SHALL: Her ajan ailesi için bağımlı olduğu diğer ajan aileleri en fazla 8 doğrudan bağımlılık ile sınırlandırılmalıdır; 8’i aşan bağımlılık grafiği 3 iş günü içinde mimari incelemeye alınmalı ve yeni sürüm dağıtımı mimari onay olmadan yapılmamalıdır. (Otomatik: ajan bağımlılık grafiği ve release kontrol kayıtlarından kontrol edilir.)
   - MUST: Kritik seviye "yüksek" veya "kritik" olan ajan aileleri için owner rolü boş bırakılamaz ve aynı owner rolü en fazla 12 aktif kritik aileye atanabilir; 12 sınırı aşıldığında 5 iş günü içinde owner yeniden dağıtımı yapılmalıdır. (Otomatik: portföy kayıtları ve rol atama sisteminden kontrol edilir.)
   - SHALL: Her ajan ailesi için yaşam döngüsü durumu yalnız `taslak`, `degerlendirme`, `staging`, `uretim`, `pasif`, `kapatiliyor`, `kapatildi` değerlerinden biri olmalıdır; bu liste dışındaki durumlar 1 saniye içinde geçersiz sayılmalı ve kaydı oluşturan işlem reddedilmelidir. (Otomatik: portföy durum alanı validasyonundan kontrol edilir.)
   - MUST: Portföyde "kapatiliyor" durumuna alınan bir ajan ailesi için en geç 15 gün içinde veri, kimlik, görev ve bağımlılık temizleme planı oluşturulmalı; planı olmayan aile 15. gün sonunda otomatik kapatma onayı alamamalıdır. (Otomatik: portföy kapanış kayıtları ve workflow loglarından kontrol edilir.)
   - SHALL: Çeyreklik portföy gözden geçirmesinde, toplam bütçenin en yüksek %70’ini tüketen ilk 15 ajan ailesinin her biri için iş değeri, hata sıklığı, maliyet eğilimi ve bağımlılık karmaşıklığı değerlendirmesi yapılmalı; değerlendirme kaydı bulunmayan aileler için yeni yatırım talebi aynı çeyrekte reddedilmelidir. (Manuel: portföy kurul kayıtları ve finans raporlarından kontrol edilir.)

4. ROLLER VE SORUMLULUKLAR:
   - Portföy Yöneticisi -> Her yeni ajan ailesi için en geç 2 iş günü içinde portföy kaydı açar, yaşam döngüsü durumu atar ve kapanış metriğini tanımlar; haftada 1 kez portföy sağlık raporu üretir.
   - MAS Strateji Sahibi -> Her 90 günde 1 çeyreklik portföy gözden geçirmesi yürütür; en az 15 yüksek maliyetli ajan ailesi için yatırım devam / birleştirme / kapatma kararı verir.
   - Orkestrasyon Sahibi -> Her gün ajan kullanım hacmi, bağımlılık grafiği ve pasif aile listesini günceller; pasif veya yinelenen aileleri 24 saat içinde portföy sistemine işaretler.
   - Güvenlik Sahibi -> Her ay pasif veya kapatılıyor durumundaki ajan ailelerinin kimlik ve erişimlerinin uygun kapatıldığını denetler; 4 saat içinde kritik ihlal kaydı açar.
   - Finans ve Veri Sahibi -> Her ay görev başına maliyet, toplam aile maliyeti ve maliyet sapma oranı raporunu üretir; ilk 15 maliyetli aileyi portföy kuruluna sunar.
   - Denetim Sorumlusu -> Her çeyrekte en az 1 portföy örneklem denetimi yapar; en az 20 aile kaydı, 10 kapanış planı ve 10 pasif aile kaydını inceler; bulguları 7 iş günü içinde raporlar.

5. İSTİSNALAR:
   - Regülasyon kaynaklı zorunlu geçiş, kritik güvenlik düzeltmesi veya birleşik geçiş dönemlerinde geçici aile limiti 15’ten 20’ye çıkarılabilir.
   - Bu istisna yalnız MAS Strateji Sahibi + Portföy Yöneticisi + Güvenlik Sahibi ortak onayı ile verilir.
   - İstisna süresi en fazla 30 takvim günü geçerlidir.
   - İstisna kaydında etkilenen aile sayısı, beklenen kapanış tarihi ve geçici maliyet etkisi yüzdesi yazılmadan istisna geçerli sayılmaz.
   - Aynı portföy kümesi için aynı 90 günlük dönem içinde en fazla 1 istisna verilebilir.

6. YAPTIRIMLAR:
   - Portföy kaydı eksik olan ajan ailesi staging ve üretim ortamına dağıtılamaz; çalışıyorsa 60 saniye içinde görev kabulü durdurulur.
   - Pasif olduğu halde 90 gün boyunca kapatılmayan ailelerin kimlikleri iptal edilir, kuyruk abonelikleri kaldırılır ve yeni görev ataması engellenir.
   - Yinelenen ajan ailesi için 10 iş günü içinde karar üretilmezse ilgili aileye yeni özellik geliştirme bütçesi 14 gün süreyle dondurulur.
   - İnsan tarafında owner rolü 4 saat içinde bilgilendirilir; 2 tekrar eden portföy ihlali sonrası yetki gözden geçirme açılır, 3 tekrar eden ihlal sonrası zorunlu portföy yönetişimi eğitimi atanır.

7. UYGULAMA ADIMLARI:
   - Portföy yönetim sistemine zorunlu alan validasyonu, yaşam döngüsü enum kontrolü ve owner limit kontrolü eklenir.
   - CI/CD hattına portföy kaydı, örnek giriş/çıkış seti ve kapanış metriği olmayan ajan ailelerini reddeden otomatik adım eklenir.
   - Haftalık portföy sağlık puanı ve yinelenen aile tespiti için otomatik analiz görevi tanımlanır ve sonuçlar dashboard’a yazılır.
   - Pasif aileleri 45 gün, 90 gün ve kapanış eşiğine göre etiketleyen yaşam döngüsü script’i uygulanır.
   - Çeyreklik portföy kurul raporunu üreten finans, kullanım, hata ve bağımlılık birleştirme job’ı kurulur.

8. METRİK VE RAPORLAMA:
   - Metrik 1: Portföy kaydı eksik ajan ailesi sayısı (hedef: aylık 0)
   - Metrik 2: Son 45 günde görev almayan üretim aile sayısı (hedef: aylık <= 5)
   - Metrik 3: 55 puan altı portföy sağlık puanına sahip aile sayısı (hedef: çeyreklik <= 8)
   - Metrik 4: 90 gün içinde kapatılamayan pasif aile sayısı (hedef: aylık 0)
   - Metrik 5: Yinelenen ajan ailesi tespit edilip 10 iş günü içinde karar verilmeyen dosya sayısı (hedef: aylık 0)
   - Raporlama sıklığı: haftalık portföy sağlık raporu, aylık maliyet ve kullanım raporu, çeyreklik portföy kurul raporu
   - Rapor alıcıları: Portföy Yöneticisi, MAS Strateji Sahibi, Orkestrasyon Sahibi, Güvenlik Sahibi, Finans ve Veri Sahibi, Denetim Sorumlusu

9. İLİŞKİLİ POLİTİKALAR:
   - Çoklu Ajan Sistemi (MAS) Vizyon ve Strateji Politikası
   - Ajan Yatırım ve Bütçe Yönetimi Politikası
   - Kurumsal Mimari ile Uyum Politikası
   - Ajan Yetkinlik ve Olgunluk Modeli Politikası
   - Ajan Görev Devir ve Yetki Delegasyonu Politikası
   - Ajan Karantina ve Adli İzolasyon Politikası
   - Tüm agentlere politikaları uygulama politikası

10. YÜRÜRLÜK TARİHİ VE REVİZYON:
   - Yürürlük Tarihi: Yayın tarihi
   - Revizyon Sıklığı: 12 ayda 1 kez zorunlu gözden geçirme
   - Erken Revizyon Tetikleyicileri: 90 gün içinde 2 kritik portföy ihlali, aktif aile sayısında %15 artış, toplam portföy maliyetinde 60 gün içinde %12 artış, yeni düzenleyici zorunluluk

11. TANIMLAR (SÖZLÜK):
   - Portföy kaydı: Bir ajan ailesinin amacı, owner rolü, yaşam döngüsü, KPI’ları, maliyet sınıfı ve kapanış kriterlerini içeren resmi kayıt.
   - Ajan ailesi: Aynı iş hedefi veya aynı yetenek kümesi etrafında gruplanmış ajanlar topluluğu.
   - Pasif aile: Son 45 günde görev almamış ancak henüz tamamen kapatılmamış ajan ailesi.
   - Kapanış metriği: Ajan ailesinin durdurulması veya yeniden tasarlanması gerektiğini gösteren ölçülebilir eşik.
   - Yinelenen aile: Aynı giriş-çıkış ve aynı iş hedefini paylaşan, ayrı tutulduğunda portföy karmaşıklığı yaratan ajan ailesi.
   - Yaşam döngüsü durumu: Ajan ailesinin taslaktan kapatılmaya kadar resmi portföy evresini gösteren durum alanı.
   - Portföy sağlık puanı: Kullanım, maliyet, hata oranı ve başarı metriğinden türetilen 0-100 arası puan.
   - Kritik seviye: Bir ajan ailesinin iş, güvenlik, veri veya kullanıcı etkisi bakımından önem derecesi.
   - Owner rolü: İlgili ajan ailesinin işletim, gözden geçirme ve kapanış kararlarından sorumlu rol.
   - Bağımlılık grafiği: Bir ajan ailesinin kullandığı diğer ajan aileleri ve sistem bileşenleri ile ilişki haritası. 

GitHub’a işlendi:
- `docs/policies/enterprise-series/A-03-ajan-portfoy-yonetimi-politikasi.md`
- Commit: `75949ab5971f10ed48b85c0f834a931fe50d7e32`