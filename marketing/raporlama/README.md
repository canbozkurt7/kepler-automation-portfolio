[← Ana sayfa](../../README.md)

# 📊 Marketing > Raporlama

Performans verisini toplayıp rapor/dashboard haline getiren otomasyonlar.

---

## Google Ads Aylık Karşılaştırma Raporu

**Ne işe yarıyor:** Google Ads hesabındaki tüm aktif kampanyaların ay-üstü-ay (month-over-month) trafik/dönüşüm/gelir karşılaştırmasını gösteren bir grafik/rapor sayfası üreten Python scripti (sunum destesinin bir sayfasına manuel olarak eklenmek üzere).

**Tetikleyici:** Windows Task Scheduler — ayın 10'u ve 20'si, saat 11:00.

**Kullanılan araçlar/entegrasyonlar:** Google Ads API, Python (görsel/grafik üretimi).

**Akış özeti:**
- Google Ads API'den dönem karşılaştırmalı (bu ay 1→X vs geçen ay 1→X) kampanya verisi çekilir.
- Trafik, dönüşüm ve gelir için 3 ayrı tablo halinde, iyileşen/kötüleşen/yeni-aktif kampanyaları renk kodlarıyla gösteren 1920x1080 bir görsel oluşturulur.
- Görsel, sunum destesine manuel olarak eklenir (API ile otomatik sayfa üzerine yerleştirme desteklenmediği için bu adım manuel).

**Durum:** Aktif, düzenli çalışıyor.

---

## Google Ads Backfill - Report Generator (PDF)

**Ne işe yarıyor:** Google Ads hesabından geçmişe dönük haftalık kampanya/anahtar kelime/arama terimi/görünürlük verisini toplayıp veritabanına yazan, ardından aktif kampanyalar için haftalık bir performans raporu üretip PDF olarak e-posta ile gönderen bir otomasyon.

**Tetikleyici:** Haftalık zamanlanmış + manuel çalıştırma seçeneği.

**Kullanılan araçlar/entegrasyonlar:** Google Ads API, Supabase, HTML→PDF dönüştürme, Gmail, AI Agent destekli yorum bloğu.

**Akış özeti:**
- Haftalık dönemler oluşturulup sırayla işlenir (rate-limit için aralarda bekleme uygulanır).
- Kampanya/reklam grubu verisi ve anahtar kelime/arama terimi/görünürlük verisi ayrı ayrı çekilip veritabanına yazılır.
- Aktif kampanyaların son dönem verisiyle HTML rapor oluşturulur, PDF'e çevrilir.
- Rapor e-posta eki olarak gönderilir.

**Durum:** Pasif.

---

## Google Ads Backfill (Jan 26 - Today)

**Ne işe yarıyor:** Belirli bir başlangıç tarihinden bugüne kadar olan haftalık Google Ads verisini (kampanya, anahtar kelime, arama terimi, açık artırma/görünürlük istatistikleri) geriye dönük olarak veritabanına dolduran bir tek seferlik/periyodik veri tamamlama (backfill) otomasyonu.

**Tetikleyici:** Manuel çalıştırma.

**Kullanılan araçlar/entegrasyonlar:** Google Ads API, Supabase.

**Akış özeti:**
- Başlangıç tarihinden bugüne kadar olan haftalar otomatik hesaplanır.
- Her hafta için sırasıyla kampanya, anahtar kelime, arama terimi ve açık artırma görünürlüğü verisi Google Ads API'den çekilir.
- Her veri seti formatlanıp ilgili Supabase tablosuna yazılır, sonra bir sonraki haftaya geçilir.

**Durum:** Pasif (tek seferlik/manuel amaçlı).

---

## Google Analytics: Weekly Report

**Ne işe yarıyor:** Google Analytics 4'ten haftalık satın alma (purchase) verisini ülke ve trafik kaynağına göre gruplandırıp bir PDF rapor haline getiren ve e-posta ile gönderen otomasyon.

**Tetikleyici:** Zamanlanmış — haftalık, Pazartesi öğlen.

**Kullanılan araçlar/entegrasyonlar:** Google Analytics 4 API, HTML→PDF dönüştürme, Gmail.

**Akış özeti:**
- GA4'ten ülke + kaynak/kanal bazlı satın alma ve dönüşüm oranı verisi çekilir.
- Veriler ülkeye göre gruplanıp sıralanır, HTML rapor oluşturulur (özet kartlar + ülke bazlı tablolar).
- HTML, PDF'e çevrilip dosya adı tarihlenir.
- Rapor e-posta eki olarak gönderilir.

**Durum:** Pasif.

---

## PPC Marketing Dashboard

**Ne işe yarıyor:** Google Ads verisini saatlik olarak çekip bir veritabanına senkronize eden ve React tabanlı bir web arayüzünde (tarih aralığı seçimi, kampanya/kanal kırılımı ile) canlı performans dashboard'u olarak sunan, VPS üzerinde 7/24 çalışan bir servis.

**Tetikleyici:** Saatlik otomatik senkronizasyon (APScheduler) + sunucu açılışında bir kez.

**Kullanılan araçlar/entegrasyonlar:** Google Ads API, Supabase (Postgres), Python (FastAPI + APScheduler), React/TypeScript frontend, Docker, VPS.

**Akış özeti:**
- Sunucu açıldığında ve her saat başı, Google Ads API'den güncel veri çekilir ve veritabanına yazılır.
- Backend, dashboard için normalize edilmiş veriyi bir API üzerinden sunar.
- Frontend bu veriyi tarih aralığı filtresiyle grafik/tablo olarak gösterir.

**Durum:** Canlı, sürekli çalışıyor. (Meta/Yandex ve GA4/Clarity entegrasyonları için genişletme planlanıyor.)
