[Çoklu Ajan Sistemi (MAS) Vizyon ve Strateji Politikası]

1. AMAÇ: 60 ajanlı üretim uygulamasında stratejik hedeflere bağlı tüm ajan yatırımlarının, canlı ortamda aylık en az %99,90 görev tamamlama oranı ve kritik iş akışlarında en fazla %1,00 kontrolsüz sapma oranı ile yürütülmesini garanti etmektir.

2. KAPSAM:
   - Hangi ajan tipleri?
     - Veri toplayıcı ajanlar
     - Sınıflandırma ve analiz ajanları
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
     - Politika motoru
     - Kimlik ve yetki katmanı
     - Gözlemlenebilirlik altyapısı
     - Veritabanı ve nesne depoları
     - Önizleme ve yürütme çalışma zamanı katmanı
   - Hangi zaman dilimleri?
     - Üretim ortamında 7/24
     - Geliştirme, test ve staging ortamlarında iş saatleri + planlı bakım pencereleri
     - Bakım pencereleri en fazla haftada 1 kez ve en fazla 120 dakika

3. KURALLAR:
   - MUST: Kurumsal MAS strateji belgesi, her 12 ayda 1 kez tam gözden geçirmeden geçmeli ve her gözden geçirme çıktısında en az 5 ölçülebilir iş hedefi bulunmalıdır. (Manuel: strateji belgesi ve yönetim kurulu kayıtlarından kontrol edilir.)
   - SHALL: Üretimde çalışan ajan sayısı, onaylı portföy kaydı dışında 60 temel ajan + en fazla 12 geçici ajan sınırını aşmamalıdır; 72 saati aşan geçici ajanlar kalıcı portföy incelemesine alınmalıdır. (Otomatik: ajan kayıt defteri ve orkestrasyon loglarından kontrol edilir.)
   - MUST: Her ajan ailesi, canlıya alınmadan önce en az 1 iş hedefi, 1 sahip rol, 1 başarı metriği ve 1 kapanış metriği ile portföy kaydına bağlanmalıdır. Eksik alan sayısı 1 bile olsa canlıya geçiş reddedilmelidir. (Otomatik: portföy kayıt şeması validasyonundan kontrol edilir.)
   - SHALL: Kritik iş akışlarında görev tamamlama oranı 30 günlük hareketli pencerede %99,90’ın altına düşerse 24 saat içinde stratejik kapasite ve mimari gözden geçirme oturumu açılmalıdır. (Otomatik: görev tamamlama metriklerinden kontrol edilir.)
   - MUST: Aynı anda çalışan ajan örneği başına ortalama CPU kullanım hedefi 5 dakikalık pencerede %70’in, bellek kullanım hedefi %75’in üzerine 3 ardışık ölçüm boyunca çıkarsa kapasite planlama alarmı oluşturulmalıdır. (Otomatik: çalışma zamanı metriklerinden kontrol edilir.)
   - SHALL: Mesaj kuyruğunda tek bir iş akışı kuyruğunda bekleyen mesaj sayısı 1.500’ü aşarsa 60 saniye içinde geri basınç veya yük azaltma politikası tetiklenmelidir; 3.000’i aşan kuyruk durumunda yeni iş kabulü ilgili akış için durdurulmalıdır. (Otomatik: kuyruk metriklerinden kontrol edilir.)
   - MUST: Her ajan, kimlik doğrulama, yetki kapsamı ve görev kapsamı eşleşmeden iş başlatmamalı; eşleşmeyen isteklerin %100’ü 1 saniye içinde reddedilmelidir. (Otomatik: kimlik ve politika motoru loglarından kontrol edilir.)
   - SHALL: Yarış koşulu riski taşıyan paylaşımlı kaynaklara erişen ajan akışlarında, aynı kaynak anahtarı için eşzamanlı yazma denemesi en fazla 1 aktif yazıcı ve en fazla 2 bekleyen işlem ile sınırlandırılmalıdır; üçüncü bekleyen işlem 5 saniye içinde geri çevrilmelidir. (Otomatik: kilit yöneticisi ve veritabanı işlem loglarından kontrol edilir.)
   - MUST: Deadlock tespit süresi en fazla 10 saniye olmalı; deadlock tespit edilen akışlarda en geç 30 saniye içinde 1 işlem iptal edilmeli ve olay kaydı açılmalıdır. (Otomatik: işlem yöneticisi ve uyarı sisteminden kontrol edilir.)
   - SHALL: Aging riskini azaltmak için düşük öncelikli ajan görevleri 15 dakikadan uzun süre sırada kalmamalı; 15 dakikayı aşan her görev için öncelik 1 seviye yükseltilmeli ve 30 dakikayı aşan görevler günlük aging raporuna dahil edilmelidir. (Otomatik: görev kuyruğu ve zaman damgası kayıtlarından kontrol edilir.)
   - MUST: Ajan başına düşen ortalama aktif görev sayısı 10 dakikalık pencerede 8’i aşarsa orkestrasyon katmanı yeni görev atamalarını kademeli olarak azaltmalı; 12’yi aşarsa o ajan sınıfı için yeni görev ataması 5 dakika süreyle durdurulmalıdır. (Otomatik: orkestrasyon metriklerinden kontrol edilir.)
   - SHALL: Stratejik olmayan veya onaysız ajan denemeleri, staging ve üretim ortamında 0 tolerans ile engellenmeli; tespit edilen her onaysız ajan örneği 60 saniye içinde karantinaya alınmalı ve 4 saat içinde inceleme kaydı açılmalıdır. (Otomatik: ajan kayıt defteri, servis keşfi ve olay loglarından kontrol edilir.)

4. ROLLER VE SORUMLULUKLAR:
   - MAS Strateji Sahibi -> 12 ayda 1 kurumsal strateji gözden geçirmesi yapar, her çeyrekte 1 portföy uyum raporu üretir, her raporda en az 5 stratejik KPI yayınlar.
   - Orkestrasyon Sahibi -> Haftada 1 kez ajan yük dağılımı, aging, queue buildup ve concurrency raporu üretir; kritik eşik aşımlarında 24 saat içinde düzeltici aksiyon kaydı açar.
   - Güvenlik Sahibi -> Her ay kimlik taklidi, yetki ihlali ve spoofing girişimlerini inceleyen 1 güvenlik uygunluk raporu üretir; kritik bulguları 4 saat içinde olay kaydına bağlar.
   - Veri ve Gözlemlenebilirlik Sahibi -> Günlük olarak görev tamamlama oranı, kuyruk şişmesi, ajan başına yük ve başarısız kimlik doğrulama sayılarını toplar; haftalık dashboard güncellemesi yayınlar.
   - Portföy Yöneticisi -> Her yeni ajan veya ajan ailesi için en geç 2 iş günü içinde portföy kaydı açar, sahip rolü atar, iş hedefi ve kapanış metriği olmayan ajanları canlıya göndermez.
   - Denetim Sorumlusu -> Aylık olarak en az 1 örneklem denetimi yapar; denetimde en az 10 ajan kaydı, 10 görev kaydı ve 5 olay kaydını inceler; bulguları 5 iş günü içinde yazılı rapora dönüştürür.

5. İSTİSNALAR:
   - Planlı büyük geçiş veya toplu veri taşıma pencerelerinde, geçici ajan sayısı sınırı 12’den 20’ye çıkarılabilir.
   - Bu istisna yalnız MAS Strateji Sahibi + Orkestrasyon Sahibi + Güvenlik Sahibi ortak onayı ile verilir.
   - İstisna süresi en fazla 72 saat geçerlidir.
   - İstisna kaydı açılmadan ve bitiş zamanı yazılmadan istisna kullanılamaz.
   - Aynı takvim ayı içinde aynı sistem bileşeni için en fazla 1 istisna verilebilir.

6. YAPTIRIMLAR:
   - Kural ihlali durumunda, onaysız ajan örneği 60 saniye içinde karantinaya alınır, görev ataması durdurulur ve kimlik bilgileri iptal edilir.
   - Stratejik hedefe bağlı olmayan ajan ailesi staging ve üretim dağıtım hattında otomatik olarak reddedilir.
   - Queue buildup, deadlock veya aging sınırı art arda 3 kez aşılırsa ilgili ajan sınıfı için otomatik kapasite düşürme uygulanır ve yeni görev kabulü en az 5 dakika durur.
   - İnsan tarafında ilgili sahip rol 4 saat içinde bilgilendirilir, tekrar eden ihlal 2 kez yaşanırsa yetki gözden geçirme açılır, 3 kez yaşanırsa zorunlu yeniden eğitim atanır.

7. UYGULAMA ADIMLARI:
   - Orkestrasyon katmanına ajan kayıt defteri zorunluluğu eklenir; kayıtsız ajan örneği başlatma çağrıları deployment pipeline içinde reddedilir.
   - Mesaj kuyruğu, aging, deadlock ve concurrency eşikleri için monitoring dashboard ve alarm kuralları tanımlanır.
   - Portföy kaydı, iş hedefi, owner, KPI ve kapanış metriği olmayan ajan ailelerini reddeden schema validation script’i CI/CD hattına eklenir.
   - Yetki kapsamı ve görev kapsamı uyuşmazlığını 1 saniye içinde reddeden policy-engine kural seti uygulanır.
   - Aylık denetim için otomatik rapor üretimi yapan bir raporlama görevi tanımlanır ve sonuçlar yönetim klasörüne arşivlenir.

8. METRİK VE RAPORLAMA:
   - Metrik 1: 30 günlük hareketli görev tamamlama oranı (hedef: >= %99,90)
   - Metrik 2: Kuyrukta 15 dakikadan uzun bekleyen görev sayısı (hedef: günlük <= 25)
   - Metrik 3: Onaysız ajan başlatma denemesi sayısı (hedef: aylık 0)
   - Metrik 4: Deadlock tespiti sonrası 30 saniye içinde çözülmeyen olay sayısı (hedef: aylık 0)
   - Raporlama sıklığı: günlük operasyon dashboard’u, haftalık teknik özet, aylık yönetim raporu
   - Rapor alıcıları: MAS Strateji Sahibi, Orkestrasyon Sahibi, Güvenlik Sahibi, Denetim Sorumlusu

9. İLİŞKİLİ POLİTİKALAR:
   - Ajan Portföy Yönetimi Politikası
   - Kurumsal Mimari ile Uyum Politikası
   - Ajan Kimlik Doğrulama ve Yetki Taklidi Önleme Politikası
   - Ajan Koordinasyon ve Senkronizasyon Politikası
   - Ajan Risk Değerlendirme ve Önceliklendirme Politikası
   - Ajan Karantina ve Adli İzolasyon Politikası
   - Tüm agentlere politikaları uygulama politikası

10. YÜRÜRLÜK TARİHİ VE REVİZYON:
   - Yürürlük Tarihi: Yayın tarihi
   - Revizyon Sıklığı: 12 ayda 1 kez zorunlu gözden geçirme
   - Erken Revizyon Tetikleyicileri: 30 gün içinde 2 kritik olay, ajan sayısında %20 artış, kritik regülasyon değişikliği, yeni üretim bölgesi açılması

11. TANIMLAR (SÖZLÜK):
   - Ajan: Tanımlı bir görevi yerine getiren, kimlikli ve izlenebilir yazılım bileşeni.
   - MAS: Çoklu ajan sistemi; birden fazla ajanın ortak hedefler için eşgüdümlü çalıştığı mimari.
   - Queue buildup: Mesaj kuyruğunda bekleyen işlerin tanımlı eşik üzerinde birikmesi.
   - Aging: Düşük öncelikli görevlerin uzun süre iş alamadan beklemesi.
   - Deadlock: İki veya daha fazla işlemin birbirini beklediği ve ilerlemenin durduğu durum.
   - Spoofing: Ajanın veya aktörün sahte kimlikle sisteme erişmeye çalışması.
   - Portföy kaydı: Ajan ailesinin amacı, sahibi, KPI’ları ve yaşam döngüsünü tutan resmi kayıt.
   - Kritik iş akışı: Hata oluştuğunda hizmet, güvenlik, veri veya kullanıcı etkisi yüksek olan süreç.
   - Karantina: Ajan örneğinin görev, ağ veya kimlik yeteneklerinin sistem tarafından kısıtlanması.
   - Kapanış metriği: Bir ajan ailesinin durdurulması, küçültülmesi veya yeniden tasarlanması gerektiğini gösteren eşik metrik.
