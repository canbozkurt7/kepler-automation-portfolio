[← Ana sayfa](../../README.md)

# 📊 Marketing > İstihbarat

Rakip ve pazar verisini otomatik toplayan sistemler.

---

## Google Ads Competitor Keyword Monitor

**Ne işe yarıyor:** Manuel olarak belirlenmiş bir anahtar kelime listesi için haftalık olarak canlı Google arama sonuçlarındaki reklamları tarayan, hangi rakiplerin hangi kelimede reklam verdiğini ve reklam metni/pozisyon değişikliklerini hafta-üstü-hafta karşılaştırıp anlamlı bir değişiklik olduğunda AI destekli bir özet e-posta gönderen bir rekabet istihbaratı sistemi.

**Tetikleyici:** Zamanlanmış — haftalık.

**Kullanılan araçlar/entegrasyonlar:** SerpAPI (canlı Google arama sonuçları), Supabase, AI Agent (LLM destekli analiz), Gmail.

**Akış özeti:**
- Supabase'deki aktif anahtar kelime listesi okunur.
- Her kelime için SerpAPI üzerinden o anki Google reklamları (pozisyon, marka, başlık, açıklama) çekilir ve reklamveren adı normalize edilir.
- Sonuçlar Supabase'e kaydedilir; aynı kelimenin önceki taramasıyla karşılaştırılıp yeni giren/çıkan reklamverenler, başlık değişiklikleri ve pozisyon kaymaları tespit edilir.
- Anlamlı bir değişiklik varsa, bir AI Agent bulguları yorumlayıp özet bir analiz e-postası hazırlar.

**Durum:** Aktif.

---

## Hotel Competitive Price Monitoring

**Ne işe yarıyor:** SAW/RIX/KUL havalimanı lokasyonlarındaki rakip otellerin fiyatlarını haftalık olarak tarayıp kendi fiyatlarınla karşılaştıran, pazar ortalaması ve fiyat değişikliklerini bir e-posta raporunda özetleyen bir rekabetçi fiyat izleme sistemi.

**Tetikleyici:** Zamanlanmış — haftalık, Pazartesi 08:00.

**Kullanılan araçlar/entegrasyonlar:** Apify (Booking.com scraping), Supabase, Google Sheets (kendi fiyatların), Gmail.

**Akış özeti:**
- Check-in/check-out tarihleri otomatik hesaplanır (bugünden +14/+15 gün).
- Her lokasyon için Apify üzerinden Booking.com'daki otel fiyatları taranıp Supabase'e kaydedilir.
- Bu haftaki ve geçen haftaki veriler karşılaştırılıp fiyat değişiklikleri tespit edilir; kendi fiyatınla pazar ortalaması karşılaştırılıp konumun (üstünde/altında/eşit) belirlenir.
- Sonuçlar lokasyon bazlı tablolar halinde HTML e-posta raporuna dönüştürülüp gönderilir.

**Durum:** Aktif.

---

## 4 Track Competitor Website Updates

**Ne işe yarıyor:** Bir rakip/referans web sitesinin fiyatlandırma sayfasını düzenli olarak AI destekli scraping ile tarayıp fiyat/plan değişikliği olup olmadığını tespit eden, değişiklik varsa kayıt tablosunu güncelleyen genel amaçlı bir fiyat takip şablonu.

**Tetikleyici:** Zamanlanmış — günlük.

**Kullanılan araçlar/entegrasyonlar:** AI Agent (LLM destekli sayfa okuma/ayrıştırma), bir proxy/scraping servisi, Google Sheets.

**Akış özeti:**
- Takip edilecek URL ve parametreler tanımlanır.
- Google Sheets'teki son bilinen fiyat verisi okunur.
- AI Agent, hedef sayfayı okuyup plan adı/fiyat/özellik bilgisini yapılandırılmış veriye çevirir.
- Yeni veri eskisiyle karşılaştırılır; fark varsa Google Sheets güncellenir, aynıysa hiçbir şey yapılmaz.

**Durum:** Aktif. (Genel amaçlı bir şablon; farklı rakip/ürün sayfaları için yeniden kullanılabilir.)

---

## Meta Ads Creative Fatigue Detection

**Ne işe yarıyor:** Meta (Facebook/Instagram) reklamlarının performansını günlük olarak izleyip hangi reklam kreatiflerinin "yorulduğunu" (creative fatigue — tekrar izlenme yorgunluğu) otomatik tespit eden ve ekibe Slack üzerinden uyarı gönderen bir sistem.

**Tetikleyici:** Zamanlanmış — haftalık, Pazartesi 08:00.

**Kullanılan araçlar/entegrasyonlar:** Meta Marketing API (Insights), Supabase, Slack, Gmail.

**Akış özeti:**
- Son 14 günün günlük reklam performans verisi (CTR, frequency, CPM, gösterim vb.) Meta API'den çekilir ve veritabanına yazılır.
- Her reklam için tüm geçmiş veri çekilip 3 sinyal hesaplanır: CTR düşüşü (%20+), yüksek frequency (aynı kişiye 3+ gösterim), CPM artışı + CTR düşüşü kombinasyonu.
- 2 veya daha fazla sinyal tetiklenirse reklam "yorgun" sayılır.
- Aynı gün için daha önce uyarı gönderilmediyse (tekrar önleme kontrolü), Slack kanalına ve e-postaya uyarı gönderilir, log tutulur.

**Durum:** Aktif.

---

## Google Trends

**Ne işe yarıyor:** Havalimanı "nap room" / kapsül otel kavramıyla ilgili arama ilgisini (search interest) farklı lokasyonlar için karşılaştırıp bir Google Sheet'e zaman serisi olarak kaydeden basit bir pazar-ilgisi takip aracı.

**Tetikleyici:** Manuel çalıştırma.

**Kullanılan araçlar/entegrasyonlar:** SerpAPI (Google Trends verisi), Google Sheets.

**Akış özeti:**
- Belirlenen arama terimleri için son 12 ayın haftalık/aylık ilgi endeksi çekilir.
- Sonuçlar tarih bazlı satırlara dönüştürülüp Google Sheets'e eklenir.

**Durum:** Aktif, manuel/periyodik kontrol amaçlı.

---

## kepler-nationality-ad-copy (Skill)

**Ne işe yarıyor:** SAW (İstanbul), KUL (Kuala Lumpur) ve RIX (Riga) havalimanı kapsül otel kampanyaları için, her lokasyonun gerçek misafir milliyeti ve arama dili dağılımına göre farklılaştırılmış (tek bir genel script yerine) yüksek CTR'li Google Ads başlık/açıklama metinleri üreten bir Claude Code yeteneği (skill).

**Tetikleyici:** Talep üzerine ("SAW için headline yaz" gibi).

**Kullanılan araçlar/entegrasyonlar:** Claude Code skill sistemi, Google Ads kampanya bağlamı.

**Akış özeti:**
- Kullanıcı bir lokasyon (SAW/KUL/RIX) ve kampanya tipi (Search/PMax) belirtir.
- Skill, o lokasyonun misafir milliyet/dil profiline uygun başlık, uzun başlık ve açıklama metinleri üretir.

**Durum:** Aktif olarak kullanılıyor.
