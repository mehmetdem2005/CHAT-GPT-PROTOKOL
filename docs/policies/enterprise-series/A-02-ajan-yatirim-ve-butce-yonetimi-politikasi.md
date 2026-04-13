[Ajan Yatırım ve Bütçe Yönetimi Politikası]

1. AMAÇ: 60 ajanlı üretim uygulamasında tüm ajan yatırımlarının, yıllık onaylı bütçe içinde kalarak görev başına maliyeti kritik iş akışlarında en fazla %10 sapma ile yönetilmesini garanti etmektir.

2. KAPSAM:
   - Hangi ajan tipleri?
     - Veri toplayıcı ajanlar
     - Analiz ve sınıflandırma ajanları
     - Karar ajanları
     - Planlama ve orkestrasyon ajanları
     - Eylem ajanları
     - Doğrulama, denetim ve geri besleme ajanları
   - Hangi ortamlar?
     - Geliştirme
     - Test
     - Staging
     - Üretim
   - Hangi sistem bileşenleri?
     - API gateway
     - Mesaj kuyruğu
     - Orkestrasyon katmanı
     - Token ve model erişim katmanı
     - Görev planlama servisi
     - Çalışma zamanı kümeleri
     - Gözlemlenebilirlik altyapısı
     - Maliyet raporlama veri ambarı
     - Nesne depoları ve veritabanları
   - Hangi zaman dilimleri?
     - Üretim ortamında 7/24
     - Bütçe izleme ve alarm kuralları 7/24
     - Aylık maliyet kapanışı her ayın ilk 3 iş günü içinde
     - Çeyreklik yatırım gözden geçirmesi her 90 günde 1 kez

3. KURALLAR:
   - MUST: Her ajan ailesi, canlıya alınmadan önce yıllık bütçe tavanı, aylık bütçe tavanı ve görev başına hedef maliyet ile maliyet kayıt sistemine bağlanmalıdır; bu üç alandan herhangi biri eksikse dağıtım hattı 1 dakika içinde reddedilmelidir. (Otomatik: bütçe kayıt şeması ve CI/CD validasyon loglarından kontrol edilir.)
   - SHALL: Tek bir ajan ailesinin aylık toplam harcaması, onaylı aylık bütçesinin %105’ini aşamaz; %95 eşiği geçildiğinde uyarı, %100 eşiği geçildiğinde inceleme kaydı, %105 eşiği geçildiğinde yeni görev kabulü ilgili aile için en az 15 dakika durdurulmalıdır. (Otomatik: maliyet metrikleri ve orkestrasyon loglarından kontrol edilir.)
   - MUST: Üretim ortamında görev başına ortalama token/API maliyeti, 7 günlük hareketli pencerede onaylı hedefin %10 üzerine çıktığında 24 saat içinde maliyet neden analizi açılmalı; %20 üzerine çıktığında ilgili ajan ailesi için yeni deneysel görevler durdurulmalıdır. (Otomatik: maliyet veri ambarı ve görev yürütme kayıtlarından kontrol edilir.)
   - SHALL: Aynı iş hedefini yerine getiren iki ajan varyantı bulunduğunda, görev hacmi günlük en az 1.000 ise daha pahalı varyantın maliyeti ucuz varyantın %120’sini aşamaz; bu eşik aşıldığında 3 iş günü içinde portföy optimizasyon kararı alınmalıdır. (Otomatik: görev sayacı ve varyant maliyet raporlarından kontrol edilir.)
   - MUST: Üretim ortamında boşta çalışan ajan örnekleri, CPU kullanımının %5 altında ve aktif görev sayısının 0 olduğu 10 dakikalık pencere boyunca devam ederse 2 dakika içinde sonlandırılmalı; aynı ajan ailesi için bir saat içinde en fazla 3 otomatik yeniden başlatma yapılmalıdır. (Otomatik: runtime metrikleri ve yaşam döngüsü loglarından kontrol edilir.)
   - SHALL: Mesaj kuyruğunda bekleyen maliyet üretici görevler 2.000 adedi aştığında sistem ilgili düşük öncelikli görevlerin en az %20’sini gecikmeli yürütme havuzuna taşımalıdır; kuyruk 4.000 adedi aşarsa yeni düşük öncelikli görev kabulü 10 dakika süreyle durdurulmalıdır. (Otomatik: kuyruk metrikleri ve orkestrasyon karar loglarından kontrol edilir.)
   - MUST: Deneysel veya araştırma sınıfındaki ajan çalıştırmaları, aylık toplam agent bütçesinin %8’ini aşamaz; %8 eşiği geçildiğinde ilgili kategori için yeni çalıştırmalar aynı takvim ayı sonuna kadar engellenmelidir. (Otomatik: kategori bazlı bütçe raporlarından kontrol edilir.)
   - SHALL: Her ajan ailesi için aylık en az 1 maliyet-verimlilik puanı hesaplanmalıdır; bu puan, görev başına maliyet, başarı oranı ve yeniden deneme oranı kullanılarak 0-100 aralığında üretilmeli ve 60 puanın altında kalan aileler 5 iş günü içinde portföy incelemesine alınmalıdır. (Otomatik: maliyet modeli ve görev performans raporlarından kontrol edilir.)
   - MUST: Üçüncü taraf model veya araç entegrasyonları için sözleşmesiz kullanım 0 tolerans ile engellenmeli; lisans veya kota tanımı bulunmayan entegrasyon çağrılarının %100’ü 1 saniye içinde reddedilmelidir. (Otomatik: entegrasyon kimlik ve lisans kontrol loglarından kontrol edilir.)
   - SHALL: Aynı ajan ailesi için 30 günlük dönemde yeniden deneme oranı %12’yi aşarsa maliyet sızıntısı incelemesi açılmalı; %20’yi aşarsa ilgili ajan ailesi için concurrency sınırı mevcut değerin %25 altına indirilmelidir. (Otomatik: görev yürütme logları ve yeniden deneme metriklerinden kontrol edilir.)
   - MUST: Her çeyrekte en az 1 kez, toplam agent bütçesinin en yüksek %80’ini tüketen ilk 10 ajan ailesi için yatırım getirisi değerlendirmesi yapılmalı; ROI hesaplaması eksik olan aileler sonraki çeyrek için yeni bütçe artışı alamamalıdır. (Manuel: finans gözden geçirme kayıtları ve portföy raporlarından kontrol edilir.)
   - SHALL: Onaysız bütçe aşımı yapan bir ajan ailesi 30 gün içinde 2 kez %105 eşiğini geçerse, ilgili aile için yeni özellik geliştirme bütçesi 14 gün süreyle dondurulmalı ve zorunlu maliyet azaltma planı açılmalıdır. (Otomatik: bütçe alarm kayıtları ve portföy yönetim sisteminden kontrol edilir.)

4. ROLLER VE SORUMLULUKLAR:
   - MAS Finans Sahibi -> Her ayın ilk 3 iş günü içinde aylık agent harcama kapanış raporu üretir, her raporda en az 10 en yüksek harcama kalemini listeler ve bütçe sapmalarını yüzde olarak yayımlar.
   - Portföy Yöneticisi -> Her yeni ajan ailesi için 2 iş günü içinde bütçe tavanı, görev başına hedef maliyet ve ROI kategorisi tanımlar; eksik tanımlı aileleri canlıya göndermez.
   - Orkestrasyon Sahibi -> Günlük olarak agent başına aktif yük, idle süre, concurrency ve yeniden deneme oranı raporu üretir; eşik aşımı olduğunda 24 saat içinde teknik düzeltme kaydı açar.
   - Güvenlik ve Lisans Sahibi -> Haftalık olarak üçüncü taraf araç ve model çağrılarını inceler; lisanssız veya kotasız entegrasyon denemelerini aynı iş günü içinde engelleme raporuna bağlar.
   - Veri ve Gözlemlenebilirlik Sahibi -> 24 saatte 1 maliyet dashboard’unu günceller; görev başına maliyet, queue buildup ve idle termination olaylarını saklar ve aylık arşiv oluşturur.
   - İç Denetim Sorumlusu -> Her çeyrekte en az 1 denetim örneklemi yapar; en az 12 ajan ailesi, 20 bütçe alarmı ve 10 lisans kontrol kaydını inceler; bulguları 7 iş günü içinde yazılı rapora dönüştürür.

5. İSTİSNALAR:
   - Zorunlu üretim kesintisi, regülasyon kaynaklı acil değişiklik veya kritik güvenlik olayında, deneysel olmayan ajan aileleri için aylık bütçe aşım limiti %105’ten %112’ye çıkarılabilir.
   - Bu istisna yalnız MAS Finans Sahibi + Güvenlik Sahibi + Portföy Yöneticisi ortak onayı ile verilir.
   - İstisna süresi en fazla 14 takvim günü geçerlidir.
   - İstisna kaydında başlangıç zamanı, bitiş zamanı, etkilenen ajan aileleri ve beklenen ek maliyet yüzdesi yazılmadan istisna geçerli sayılmaz.
   - Aynı ajan ailesi için aynı çeyrekte en fazla 1 istisna tanımlanabilir.

6. YAPTIRIMLAR:
   - Kural ihlali durumunda bütçe tavanını aşan ajan ailesi için yeni düşük öncelikli görev kabulü otomatik olarak durdurulur, concurrency sınırı düşürülür ve deneysel akışlar kapatılır.
   - Lisanssız üçüncü taraf çağrısı tespit edilen entegrasyon kimliği 1 saniye içinde iptal edilir ve ilgili çağrı yolu karantinaya alınır.
   - Aynı ajan ailesi 30 gün içinde 2 kez onaysız aşım yaparsa yeni özellik geliştirme bütçesi 14 gün dondurulur ve zorunlu maliyet azaltma planı açılır.
   - İnsan tarafında ilgili sahip roller 4 saat içinde bilgilendirilir; 2 tekrar eden ihlal sonrası yetki gözden geçirme, 3 tekrar eden ihlal sonrası zorunlu maliyet ve kapasite eğitimi atanır.

7. UYGULAMA ADIMLARI:
   - Her ajan ailesi için bütçe tavanı, görev başına hedef maliyet, ROI sınıfı ve lisans durumu alanlarını zorunlu yapan portföy kayıt şeması uygulanır.
   - Orkestrasyon katmanına idle termination, concurrency düşürme, deneysel görev engelleme ve bütçe alarmı tetikleyicileri eklenir.
   - Maliyet veri ambarına günlük görev bazlı maliyet, token tüketimi, yeniden deneme oranı ve queue buildup verisini aktaran ETL görevi kurulur.
   - CI/CD hattına, bütçe kaydı ve lisans kaydı olmayan ajan ailelerini reddeden kontrol adımı eklenir.
   - Finans ve operasyon ekipleri için haftalık maliyet dashboard’u ve aylık yönetim raporu otomatik üretilir.

8. METRİK VE RAPORLAMA:
   - Metrik 1: Aylık bütçe aşım oranı (hedef: ajan ailesi başına <= %5)
   - Metrik 2: Görev başına ortalama maliyet sapması (hedef: 7 günlük pencerede <= %10)
   - Metrik 3: Idle termination sonrası 10 dakika içinde tekrar boşa düşen ajan sayısı (hedef: haftalık <= 15)
   - Metrik 4: Lisanssız entegrasyon çağrı sayısı (hedef: aylık 0)
   - Metrik 5: Yeniden deneme oranı %12 üzerinde olan ajan ailesi sayısı (hedef: aylık <= 3)
   - Raporlama sıklığı: günlük operasyon dashboard’u, haftalık maliyet özeti, aylık yönetim raporu, çeyreklik yatırım gözden geçirme raporu
   - Rapor alıcıları: MAS Finans Sahibi, Portföy Yöneticisi, Orkestrasyon Sahibi, Güvenlik ve Lisans Sahibi, İç Denetim Sorumlusu

9. İLİŞKİLİ POLİTİKALAR:
   - Ajan Portföy Yönetimi Politikası
   - Ajan Token / API Kullanım Kotası Politikası
   - Ajan Boşta Kalma (Idle) Sonlandırma Politikası
   - Ajan Görev Başına Maliyet Muhasebesi Politikası
   - Ajan Üçüncü Parti Araç Entegrasyon Lisans Politikası
   - Ajan Kapasite Planlama Politikası
   - Tüm agentlere politikaları uygulama politikası

10. YÜRÜRLÜK TARİHİ VE REVİZYON:
   - Yürürlük Tarihi: Yayın tarihi
   - Revizyon Sıklığı: 12 ayda 1 kez zorunlu gözden geçirme
   - Erken Revizyon Tetikleyicileri: 30 gün içinde 2 kritik bütçe ihlali, üçüncü taraf lisans modelinde değişiklik, toplam ajan harcamasında 60 gün içinde %15 artış, yeni üretim bölgesi açılması

11. TANIMLAR (SÖZLÜK):
   - Ajan ailesi: Aynı iş hedefi için çalışan ve ortak bütçe kaydı taşıyan ajan grubu.
   - Görev başına maliyet: Bir görevin tamamlanması için tüketilen toplam hesaplama, token, lisans ve altyapı maliyeti.
   - ROI: Yatırım getirisi; harcanan bütçenin ölçülebilir iş çıktısına oranı.
   - Idle termination: Boşta duran ajan örneğinin belirlenmiş eşik sonunda otomatik kapatılması.
   - Queue buildup: Görev veya mesaj kuyruğunda bekleyen işlerin eşik üstünde birikmesi.
   - Concurrency sınırı: Aynı anda işleyebilen aktif ajan veya görev sayısı limiti.
   - Deneysel ajan: Canlı iş yükünde sınırlı deneme amacıyla çalışan, kalıcı portföy statüsü almamış ajan.
   - Lisanssız entegrasyon: Sözleşmesi, kota kaydı veya kullanım hakkı tanımı bulunmayan üçüncü taraf araç veya model çağrısı.
   - Bütçe tavanı: Belirli süre içinde aşılması yasak olan onaylı maksimum harcama sınırı.
   - Maliyet sızıntısı: Başarı oranı artmadan maliyetin tekrarlı deneme, boşta çalışma veya uygunsuz araç kullanımı nedeniyle yükselmesi. 

GitHub’a işlendi:
- `docs/policies/enterprise-series/A-02-ajan-yatirim-ve-butce-yonetimi-politikasi.md`
- Commit: `1d1770485eddf46768eb8c2e77f6bf5344f41deb`