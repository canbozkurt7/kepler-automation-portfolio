[← Ana sayfa](../../README.md)

# 📊 Marketing > Kontrol

SEO/Ads sağlık kontrolü ve uyarı sistemleri.

---

## Weekly Website SEO Audit Sistemi (v3 → v4)

**Ne işe yarıyor:** Kepler Club web sitesi için düzenli, çok kaynaklı bir SEO/teknik sağlık/performans denetimi yapıp ağırlıklı bir puan (0-100, harf notu) ve AI destekli yönetici yorumu içeren bir PDF rapor üretip e-posta ile gönderen sistem. Zaman içinde birkaç iterasyonla geliştirildi: v3 klasik teknik SEO denetimini kapsıyor; v4, buna ek olarak **AI Overview / GEO risk skorlaması** (Google'ın yapay zekâ destekli arama özetlerinde görünürlük riski) ve bu riski taşıyan anahtar kelimeler için otomatik içerik önerisi üreten bir alt sistemi (bkz. DataForSEO AI Overview Advisor) devreye aldı.

**Tetikleyici:** Zamanlanmış — versiyona göre 3 günde bir veya haftalık, sabah saatlerinde.

**Kullanılan araçlar/entegrasyonlar:** Google PageSpeed Insights, Google Search Console, SSL kontrolü, UptimeRobot, robots.txt/sitemap taraması, IP/GEO tespiti, DataForSEO (v4'te), AI Agent (Anthropic Claude tabanlı "SEO & GEO Expert" danışman rolü), HTML→PDF dönüştürme, Gmail.

**Akış özeti:**
- Zamanlayıcı tetiklenince hedef site/domain ayarları yüklenir.
- Paralel olarak PageSpeed (mobil/masaüstü), site HTML'i (meta/başlık/yapısal veri), robots.txt, sitemap, SSL, uptime, Search Console ve (v4'te) GEO verisi toplanır.
- Bir puanlama motoru tüm kaynakları ağırlıklandırıp genel skor/not ve kritik sorun listesi çıkarır.
- Sonuçlardan bir HTML rapor üretilir; AI Agent bu raporu yönetici bakış açısıyla yorumlayıp yönetici özeti, fırsatlar ve stratejik öneriler ekler.
- (v4) AI Overview riski belirli bir eşiği aşarsa, DataForSEO alt iş akışı çağrılıp riskli anahtar kelimeler için içerik önerisi alınır ve rapora eklenir.
- Rapor PDF'e çevrilip e-posta ile gönderilir.

**Durum:** v3 kopyaları pasif; v4 kopyalarından biri aktif, diğeri pasif (aynı sistemin farklı test/üretim kopyaları).

---

## DataForSEO AI Overview Advisor — Sub Workflow

**Ne işe yarıyor:** SEO Audit sisteminden çağrılan, DataForSEO SERP verisi ve anahtar kelime fikirleri üzerinden Google AI Overview fırsat/risk kelimelerini tespit edip bu kelimeler için AI destekli içerik önerileri üreten bir alt (sub) iş akışı.

**Tetikleyici:** Sub-workflow — başka bir workflow'dan (SEO Audit v4) çağrılarak çalışır, kendi başına zamanlanmış tetikleyicisi yok.

**Kullanılan araçlar/entegrasyonlar:** DataForSEO API, Anthropic Claude (LLM destekli içerik önerisi).

**Akış özeti:**
- Gelen anahtar kelime listesi toplu (batch) olarak işlenir.
- Her kelime için DataForSEO üzerinden SERP kontrolü ve anahtar kelime fikirleri alınır.
- Fırsatlar filtrelenip skorlanır.
- Skorlanan fırsatlar için Claude modelinden içerik önerisi alınıp bir HTML blok halinde paketlenir, çağıran workflow'a döndürülür.

**Durum:** Aktif (yalnızca alt-workflow çağrısıyla çalışıyor).

---

## Google Ads Metric Alert

**Ne işe yarıyor:** Google Ads kampanyalarının CPA/ROAS/CPC gibi kritik metriklerini gün içinde (6 saatte bir) 3 günlük ortalamayla ve önceden belirlenen eşiklerle karşılaştırıp anormal bir sapma tespit ettiğinde, AI destekli bir yorumla birlikte e-posta uyarısı gönderen bir performans izleme sistemi. Ayrıca AB/D bölgesi (Avrupa/ABD Doğu/ABD Batı) bazında saatlik performansı da ayrıştırıyor.

**Tetikleyici:** Zamanlanmış — her 6 saatte bir.

**Kullanılan araçlar/entegrasyonlar:** Google Ads API, AI Agent (LLM destekli yorum), Gmail.

**Akış özeti:**
- Bugünkü ve son 3 günün kampanya metrikleri ile saatlik segment verisi Google Ads API'den çekilir.
- CPA/ROAS/CPC için hem sabit eşik hem de 3 günlük ortalamaya göre değişim kontrolü yapılır; bölge bazlı saatlik performans ayrıca hesaplanır.
- Eşik/değişim aşımı olan kampanyalar için bir AI Agent, sapmanın olası nedenini ve önerilen aksiyonları içeren bir yorum üretir.
- Uyarılar tek bir e-postada toplanıp gönderilir.

**Durum:** Pasif.

---

## Upload Keywords to Google Ads

**Ne işe yarıyor:** Google Ads hesabındaki mevcut anahtar kelimeleri düzenli olarak çekip, rakip/anahtar kelime izleme sistemlerinin (bkz. İstihbarat kategorisi) kullandığı takip listesine otomatik olarak senkronize eden bir köprü otomasyonu.

**Tetikleyici:** Zamanlanmış — haftalık.

**Kullanılan araçlar/entegrasyonlar:** Google Ads API, Supabase.

**Akış özeti:**
- Google Ads hesabındaki tüm anahtar kelimeler ve durumları (aktif/duraklatılmış/arşivlenmiş) çekilir.
- Her kelime, takip listesi için gereken standart alanlarla (lokasyon, dil, cihaz, öncelik vb.) zenginleştirilir.
- Supabase'deki takip tablosuna yazılır.

**Durum:** Pasif.

---

## marketing-context-control (Skill)

**Ne işe yarıyor:** Kepler Club performans pazarlama ve misafir sorularında doğru bağlamı otomatik çeken bir Claude Code yeteneği — hem Supabase'deki geçmiş/normalize veriye hem de Google Ads API'den canlı kampanya/keyword/arama terimi verisine erişip soruya uygun context'i getiriyor.

**Tetikleyici:** Talep üzerine (kampanya/performans/misafir milliyeti gibi bir soru sorulduğunda otomatik devreye giriyor).

**Kullanılan araçlar/entegrasyonlar:** Supabase, Google Ads API, Claude Code skill sistemi.

**Akış özeti:**
- Kullanıcı sorusunun türüne göre ilgili veri kaynağı (geçmiş rapor mu, canlı kampanya verisi mi) belirlenir.
- İlgili tablo/GAQL sorgusu çalıştırılır, sonuç soruya bağlam olarak sunulur.

**Durum:** Aktif olarak kullanılıyor.

---

## pmax-performance-analyzer (Skill)

**Ne işe yarıyor:** Performance Max kampanyalarını (SAW/KUL/RIX) denetleyen bir Claude Code yeteneği — asset group performansı ve ROAS'ı, asset kalite derecelendirmesini (Best/Good/Low), audience signal gücünü ve aynı ürünler için standart Search/Shopping kampanyalarıyla olan cannibalization riskini analiz ediyor.

**Tetikleyici:** Talep üzerine ("PMax'i değerlendir", "cannibalization var mı" gibi).

**Kullanılan araçlar/entegrasyonlar:** Google Ads API (PMax asset group verisi), Claude Code skill sistemi.

**Akış özeti:**
- İlgili PMax kampanyasının asset group'ları ve performans verisi çekilir.
- Asset kalitesi, audience signal gücü ve Search/Shopping ile örtüşme analiz edilip özet bir değerlendirme sunulur.

**Durum:** Aktif olarak kullanılıyor.
