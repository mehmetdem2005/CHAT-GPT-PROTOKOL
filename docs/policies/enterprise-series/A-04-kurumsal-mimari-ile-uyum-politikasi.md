[Kurumsal Mimari ile Uyum Politikası]

1. AMAÇ: 60 ajanlı üretim uygulamasındaki tüm ajan ailelerinin, onaylı hedef mimariye bağlı kalmasını ve canlı ortamda mimari ihlal kaynaklı kritik dağıtım sapma oranının aylık en fazla %0,50 olmasını garanti etmektir.

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
     - API gateway
     - Mesaj kuyruğu
     - Servis keşif sistemi
     - Orkestrasyon katmanı
     - Politika motoru
     - Kimlik ve yetki katmanı
     - Veritabanları
     - Nesne depoları
     - Gözlemlenebilirlik altyapısı
     - Önizleme ve çalışma zamanı katmanı
     - CI/CD hattı
     - Mimari kayıt defteri ve modül envanteri
   - Hangi zaman dilimleri?
     - Üretim ortamında 7/24
     - Mimari uygunluk kontrolleri 7/24
     - Günlük otomatik uyum taraması her 24 saatte 1 kez
     - Haftalık mimari sapma raporu her 7 günde 1 kez
     - Çeyreklik mimari kurul gözden geçirmesi her 90 günde 1 kez

3. KURALLAR:
   - MUST: Her ajan ailesi, canlıya alınmadan önce onaylı mimari kayıt defterinde `moduleId`, `ownerRole`, `publicContracts`, `dependsOnModules`, `criticality` ve `deploymentClass` alanları ile kayıtlı olmalıdır; bu alanlardan herhangi biri eksikse dağıtım hattı 60 saniye içinde reddedilmelidir. (Otomatik: mimari kayıt şeması ve CI/CD validasyon loglarından kontrol edilir.)
   - SHALL: Bir ajan ailesi, onaylı modül envanterinde tanımlı olmayan en fazla 0 yeni dış bağımlılık ile üretime çıkabilir; 1 adet bile kayıtsız dış bağımlılık tespit edilirse ilgili sürüm staging üstü ortamlara dağıtılamaz. (Otomatik: SBOM, dependency graph ve mimari kayıt karşılaştırmasından kontrol edilir.)
   - MUST: Her ajan ailesi için doğrudan servis bağımlılığı sayısı en fazla 8 olmalıdır; 8’i aşan her bağımlılık grafiği 3 iş günü içinde mimari kurul incelemesine alınmalı ve inceleme tamamlanana kadar yeni sürüm dağıtımı durdurulmalıdır. (Otomatik: servis bağımlılık grafiği ve release gate kayıtlarından kontrol edilir.)
   - SHALL: Aynı ajan ailesi, üretimde en fazla 2 veritabanı türüne ve en fazla 1 mesajlaşma omurgasına doğrudan bağlanabilir; bu sınırlar aşıldığında mimari karmaşıklık ihlali kaydı 15 dakika içinde açılmalıdır. (Otomatik: bağlantı envanteri ve servis konfigürasyon kayıtlarından kontrol edilir.)
   - MUST: Her ajan ailesi, yalnız onaylı API contract veya mesaj şeması üzerinden veri alışverişi yapmalıdır; şema eşleşme hatası oranı 24 saatlik pencerede %0,10’u aşarsa ilgili entegrasyon 30 dakika içinde inceleme durumuna alınmalı ve yeni sürüm geçişi durdurulmalıdır. (Otomatik: schema validation logları ve entegrasyon hata metriklerinden kontrol edilir.)
   - SHALL: Üretimde çalışan her ajan örneği, `traceId`, `turnId`, `workspaceId` ve `moduleId` alanlarını %100 oranında loglamalı; bu alanlardan herhangi birinin eksik olduğu log oranı 1 saatlik pencerede %0,50’yi aşarsa mimari uygunluk alarmı oluşturulmalıdır. (Otomatik: log analizi ve observability pipeline kayıtlarından kontrol edilir.)
   - MUST: Aynı iş akışı içinde çağrılan ajanlar arasında saat sapması en fazla 250 milisaniye olmalıdır; 250 milisaniye üzerindeki zaman damgası farkı 10 dakikalık pencerede 20 olayı aşarsa senkronizasyon incelemesi 1 saat içinde açılmalıdır. (Otomatik: zaman damgası korelasyon loglarından kontrol edilir.)
   - SHALL: Üretim ortamında bir ajan ailesi, onaylı deploymentClass dışında ek çalışma zamanı sınıfı kullanamaz; `batch`, `interactive`, `critical-path`, `background` dışı bir sınıf 1 saniye içinde geçersiz sayılmalı ve başlatma işlemi reddedilmelidir. (Otomatik: runtime admission controller ve deployment manifest kayıtlarından kontrol edilir.)
   - MUST: Yarış koşulu riski taşıyan paylaşımlı yazma yüzeylerinde aynı kaynak anahtarı için en fazla 1 aktif yazar ve en fazla 2 bekleyen işlem bulunmalıdır; üçüncü bekleyen işlem 5 saniye içinde reddedilmeli ve mimari sapma kaydı açılmalıdır. (Otomatik: kilit yöneticisi ve işlem loglarından kontrol edilir.)
   - SHALL: Ajanlar arası senkron çağrılar, zincir derinliği bakımından en fazla 4 hop ile sınırlandırılmalıdır; 4 hop üzerindeki çağrı zincirleri 24 saat içinde mimari borç kaydı üretmeli ve 14 gün içinde azaltma planı açılmalıdır. (Otomatik: distributed trace kayıtlarından kontrol edilir.)
   - MUST: Çalışma zamanı bağımlı bir ajan ailesi için tek hata noktası oluşturan bileşen sayısı en fazla 1 olmalıdır; 1’den fazla kritik tek hata noktası tespit edilirse 5 iş günü içinde dayanıklılık düzeltme planı oluşturulmalı ve planı olmayan aile için yeni yatırım talebi reddedilmelidir. (Manuel: mimari kurul kayıtları ve dayanıklılık inceleme notlarından kontrol edilir.)
   - SHALL: Mimari uygunluk taraması her 24 saatte 1 kez otomatik çalıştırılmalı ve toplam kritik mimari ihlal sayısı 30 günlük pencerede 3’ü aşarsa 24 saat içinde zorunlu mimari kurul toplantısı yapılmalıdır. (Otomatik: mimari tarama job kayıtları ve kurul toplantı kayıtlarından kontrol edilir.)

4. ROLLER VE SORUMLULUKLAR:
   - Kurumsal Mimari Sahibi -> Her 90 günde 1 mimari kurul toplantısı yürütür, her toplantıda en az 10 yüksek etkili ajan ailesini inceler ve yazılı karar kaydı üretir.
   - Portföy Yöneticisi -> Her yeni ajan ailesi için 2 iş günü içinde mimari kayıt defteri girdisini açar, owner rolünü atar ve kayıt eksikse canlı geçişi engeller.
   - Orkestrasyon Sahibi -> Günlük olarak bağımlılık grafiği, senkron çağrı zinciri ve deploymentClass uyum raporu üretir; eşik ihlali olduğunda 24 saat içinde düzeltici aksiyon kaydı açar.
   - Güvenlik Sahibi -> Her ay doğrudan dış bağımlılık, onaysız entegrasyon ve tek hata noktası riski taşıyan kritik yüzeyleri inceler; kritik bulguları 4 saat içinde olay kaydına bağlar.
   - Gözlemlenebilirlik Sahibi -> Günlük olarak trace alanları, log zorunlu alanları ve hop derinliği dashboard’unu günceller; eksik alan oranı eşiklerini haftalık rapora taşır.
   - İç Denetim Sorumlusu -> Her çeyrekte en az 1 örneklem denetimi yapar; en az 15 ajan ailesi, 10 bağımlılık grafiği ve 10 mimari sapma kaydını inceler; bulguları 7 iş günü içinde raporlar.

5. İSTİSNALAR:
   - Zorunlu regülasyon geçişi, kritik güvenlik iyileştirmesi veya üretim kesintisini önleyen acil müdahale durumunda, doğrudan servis bağımlılığı sınırı 8’den 10’a çıkarılabilir.
   - Bu istisna yalnız Kurumsal Mimari Sahibi + Güvenlik Sahibi + Orkestrasyon Sahibi ortak onayı ile verilir.
   - İstisna süresi en fazla 21 takvim günü geçerlidir.
   - İstisna kaydında etkilenen modüller, ek bağımlılık sayısı, beklenen kaldırma tarihi ve risk özeti yazılmadan istisna geçerli sayılmaz.
   - Aynı ajan ailesi için aynı 90 günlük dönem içinde en fazla 1 istisna verilebilir.

6. YAPTIRIMLAR:
   - Mimari kayıt defteri eksik olan ajan ailesi staging ve üretim ortamına dağıtılamaz; çalışıyorsa 60 saniye içinde yeni görev kabulü durdurulur.
   - Kayıtsız dış bağımlılık veya onaysız deploymentClass tespit edilirse başlatma işlemi 1 saniye içinde reddedilir ve ilgili sürüm hattı bloklanır.
   - 4 hop üzeri zincirler, 14 gün içinde azaltma planı oluşturulmazsa yeni sürüm bütçesi 14 gün süreyle dondurulur.
   - İnsan tarafında ilgili owner rolü 4 saat içinde bilgilendirilir; 2 tekrar eden mimari ihlal sonrası mimari kurul zorunlu incelemesi açılır, 3 tekrar eden ihlal sonrası yetki ve sahiplik yeniden dağıtımı yapılır.

7. UYGULAMA ADIMLARI:
   - Mimari kayıt defterine zorunlu alan validasyonu, dış bağımlılık karşılaştırması ve deploymentClass enum kontrolü eklenir.
   - CI/CD hattına bağımlılık grafiği, hop derinliği ve schema contract uyumu için otomatik kapı eklenir.
   - Gözlemlenebilirlik platformuna `traceId`, `turnId`, `workspaceId`, `moduleId` alanları için eksik alan alarmı tanımlanır.
   - Günlük mimari uygunluk taraması yapan job kurulur; sonuçlar dashboard ve denetim arşivine yazılır.
   - Mimari kurul için çeyreklik rapor üreten bağımlılık, hata ve tek hata noktası birleştirme pipeline’ı oluşturulur.

8. METRİK VE RAPORLAMA:
   - Metrik 1: Kayıtsız dış bağımlılık tespit sayısı (hedef: aylık 0)
   - Metrik 2: 4 hop üzeri senkron çağrı zinciri sayısı (hedef: haftalık <= 5)
   - Metrik 3: Eksik zorunlu trace alanı içeren log oranı (hedef: saatlik <= %0,50)
   - Metrik 4: 30 günlük pencerede kritik mimari ihlal sayısı (hedef: <= 3)
   - Metrik 5: 8 bağımlılık üstü ajan ailesi sayısı (hedef: çeyreklik <= 4)
   - Raporlama sıklığı: günlük mimari uygunluk dashboard’u, haftalık teknik mimari rapor, çeyreklik mimari kurul raporu
   - Rapor alıcıları: Kurumsal Mimari Sahibi, Portföy Yöneticisi, Orkestrasyon Sahibi, Güvenlik Sahibi, Gözlemlenebilirlik Sahibi, İç Denetim Sorumlusu

9. İLİŞKİLİ POLİTİKALAR:
   - Çoklu Ajan Sistemi (MAS) Vizyon ve Strateji Politikası
   - Ajan Portföy Yönetimi Politikası
   - Ajan Protokol Standardizasyon Politikası
   - Ajan API Tasarım ve Versiyonlama Politikası
   - Ajan Koordinasyon ve Senkronizasyon Politikası
   - Ajan Donanım ve Altyapı Uyum Politikası
   - Tüm agentlere politikaları uygulama politikası

10. YÜRÜRLÜK TARİHİ VE REVİZYON:
   - Yürürlük Tarihi: Yayın tarihi
   - Revizyon Sıklığı: 12 ayda 1 kez zorunlu gözden geçirme
   - Erken Revizyon Tetikleyicileri: 30 gün içinde 3 kritik mimari ihlal, bağımlılık sayısında 60 gün içinde %20 artış, yeni üretim bölgesi açılması, çekirdek mesajlaşma omurgasının değişmesi

11. TANIMLAR (SÖZLÜK):
   - Mimari kayıt defteri: Modüller, bağımlılıklar, owner rolleri ve deployment sınıflarını tutan resmi kayıt sistemi.
   - Dış bağımlılık: Kurumsal sınır dışındaki servis, araç, model veya platform entegrasyonu.
   - DeploymentClass: Bir ajan ailesinin çalışma zamanı niteliğini belirten sınıf; örn. `interactive`, `batch`, `critical-path`, `background`.
   - Tek hata noktası: Başarısız olduğunda kritik iş akışını doğrudan durduran ve anında alternatif yolu bulunmayan bileşen.
   - Hop derinliği: Bir isteğin ajanlar veya servisler arasında geçtiği ardışık senkron çağrı sayısı.
   - Mimari sapma: Onaylı hedef mimari ile gerçek üretim davranışı arasındaki fark.
   - Şema eşleşme hatası: Bir mesajın veya API cevabının onaylı contract alanlarıyla uyuşmaması.
   - Kritik mimari ihlal: Güvenlik, tenant izolasyonu, veri bütünlüğü veya çekirdek çalışma yolunu etkileyen yüksek etkili mimari sapma.
   - Modül envanteri: Sistemde izin verilen modüllerin, sorumluluklarının ve public contract’larının listesi.
   - Uyum taraması: Mimari kurallara uyumu otomatik veya manuel denetleyen periyodik kontrol süreci. 

GitHub’a işlendi:
- `docs/policies/enterprise-series/A-04-kurumsal-mimari-ile-uyum-politikasi.md`
- Commit: `2dbd6bd460098ce9f799f6d98080b7740733db3a`