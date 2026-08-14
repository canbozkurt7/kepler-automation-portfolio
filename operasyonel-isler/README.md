[← Ana sayfa](../README.md)

# 🔧 Operasyonel İşler

Günlük operasyonu (misafir yorumları, geri bildirim, iç bilgi tabanı, iç raporlama) otomatikleştiren sistemler.

---

## Multi-Business Google Reviews

**Ne işe yarıyor:** Kepler Club'ın farklı lokasyonlarındaki (SAW, KUL Airside/Landside, RIX Airside/Landside) Google Business Profile yorumlarını otomatik izleyen, yeni yorumları tespit edip AI ile yanıt taslağı üreten, düşük puanlı yorumlarda ilgili ekibe WhatsApp üzerinden anlık uyarı gönderen ve tüm yorum verisini Google Sheets ile Supabase'e kaydeden çok işletmeli bir yorum yönetim sistemi.

**Tetikleyici:** Tasarım her lokasyon için ayrı bir Google Business Profile tetikleyicisiyle (yeni yorum geldiğinde) otomatik çalışacak şekilde; şu an prodüksiyonda manuel çalıştırma modunda.

**Kullanılan araçlar/entegrasyonlar:** Google Business Profile API, Google Sheets, Supabase, WhatsApp Business API, OpenAI destekli AI Agent (LangChain).

**Akış özeti:**
- Her lokasyondan gelen yorumlar Google Sheets'teki mevcut kayıtlarla karşılaştırılıp yeni olanlar filtrelenir.
- Yeni yorumlar standart formata çevrilip lokasyona göre yönlendirilir.
- AI Agent otomatik bir yanıt taslağı üretir, ilgili Google Business Profile üzerinden yoruma cevap olarak gönderilir.
- 5 puan altındaki yorumlar için WhatsApp üzerinden dahili ekibe uyarı gönderilir.
- Tüm yorumlar Google Sheets ve Supabase'e loglanır.

**Durum:** Aktif (üretim tetikleyicisi henüz bağlanmadı, manuel çalıştırılıyor).

---

## Aylık Resepsiyonist Yorum Sayısı

**Ne işe yarıyor:** Misafir yorumlarında geçen resepsiyonist isimlerinin ay içindeki geçme (mention) sayısını hesaplayıp ilgili yöneticilere e-posta ile rapor gönderen bir performans takip sistemi.

**Tetikleyici:** Zamanlanmış — ayın 15'i ve son günü, saat 09:00.

**Kullanılan araçlar/entegrasyonlar:** Supabase (RPC sorgusu ile mention sayımı), Gmail.

**Akış özeti:**
- Belirlenen günlerde tetiklenir, Supabase'den bir fonksiyon çağrısıyla personel bazlı mention sayıları alınır.
- Sonuçlar HTML tabloya dönüştürülür.
- İlgili yöneticilere e-posta ile gönderilir.

**Durum:** Aktif.

---

## Whatsapp Chatbot - Supabase v2

**Ne işe yarıyor:** Kepler Club'ın WhatsApp üzerinden gelen misafir mesajlarını (metin, sesli not, görsel) karşılayıp bir AI Agent aracılığıyla otomatik yanıtlayan, rezervasyon ve genel bilgi sorularına destek olan müşteri hizmetleri chatbot'u.

**Tetikleyici:** Webhook — gelen WhatsApp mesajında otomatik tetiklenir.

**Kullanılan araçlar/entegrasyonlar:** WhatsApp Business API, AI Agent (LangChain, LLM destekli), ses transkripsiyonu ve görsel analiz modelleri, Postgres tabanlı sohbet hafızası, harici bir MCP sunucusu üzerinden müsaitlik kontrolü/rezervasyon/fiyat hesaplama araçları.

**Akış özeti:**
- Gelen mesaj tipine göre (metin/ses/görsel) ayrı işlenir; ses metne, görsel analiz metnine çevrilir.
- AI Agent, yalnızca tanımlı araçlardan (doküman arama, müsaitlik kontrolü, fiyat hesaplama) beslenerek yanıt üretir — genel bilgisinden varsayım yapmaması için sınırlandırılmıştır.
- Kullanıcı bazlı konuşma geçmişi hafızada tutulur.
- Yanıt aynı WhatsApp sohbetine geri gönderilir.

**Durum:** Aktif.

---

## Upload data to Supabase

**Ne işe yarıyor:** Google Drive'a yüklenen dokümanları (SSS, oda/hizmet bilgileri vb.) otomatik olarak parçalayıp embedding'e çevirip Supabase'deki vektör veritabanına yükleyen, chatbot'ların (WhatsApp/Instagram) bilgi kaynağını güncel tutan bir altyapı otomasyonu.

**Tetikleyici:** Google Drive'da belirli bir klasöre yeni dosya eklendiğinde otomatik (polling, dakikada bir kontrol) + manuel çalıştırma seçeneği.

**Kullanılan araçlar/entegrasyonlar:** Google Drive, OpenAI Embeddings, Supabase Vector Store (LangChain).

**Akış özeti:**
- Yeni dosya tespit edilince indirilir, metin parçalarına (chunk) bölünür.
- Her parça OpenAI embedding modelinden geçirilir.
- Sonuçlar Supabase'deki `documents` tablosuna (vektör olarak) yazılır, böylece chatbot'lar bu bilgiyi arayabilir.

**Durum:** Pasif (manuel/dosya bazlı tetikleniyor).

---

## Slack → Google Sheets Misafir Geri Bildirim (OCR)

**Ne işe yarıyor:** Slack kanallarına metin veya görsel olarak düşen misafir geri bildirim formlarını otomatik ayrıştırıp (OCR ile, Türkçe destekli) Google Sheets'e kaydeden bir Node.js uygulaması.

**Tetikleyici:** Slack'e yeni mesaj/görsel düştüğünde (bot event-driven), ayrıca çevrimdışı kalınan mesajlar için yakalama (catch-up) modu var.

**Kullanılan araçlar/entegrasyonlar:** Slack API, Tesseract.js (OCR), Google Sheets API (Service Account), Node.js. Windows açılışında Task Scheduler ile otomatik başlıyor.

**Akış özeti:**
- Slack kanalındaki form gönderimleri (İsim, Tarih, Resepsiyonist, Puan vb. alanlar) tespit edilir.
- Görsel ise OCR ile metne çevrilir.
- Ayrıştırılan veri doğrulanıp tekrar kayıt önlenerek (state tracking) Google Sheets'e satır olarak eklenir.

**Durum:** Aktif, sürekli çalışıyor (Windows servis olarak).
