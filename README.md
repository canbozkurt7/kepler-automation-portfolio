# Kepler Automation Portfolio

Bu repo, Kepler Club'ın performans pazarlama, operasyon ve büyüme süreçlerinde kullandığım otomasyonların bir portfolyosudur. Otomasyonların çoğu [n8n](https://n8n.io) üzerinde çalışıyor; bazıları Python/Node.js scriptleri ve zamanlanmış görevler, bazıları da bulut tabanlı servisler (dashboard, AI asistan) olarak kurulmuş.

> **Not:** Bu repo public olduğu için hassas bilgiler (API anahtarları, e-posta adresleri, iç sistem kimlikleri, tam AI prompt metinleri) sansürlenmiş/genelleştirilmiştir. Aşağıdaki açıklamalar her otomasyonun **ne yaptığını ve nasıl çalıştığını** göstermek içindir, uygulama detayları için ham kod paylaşılmamıştır.

## İçindekiler

### 🔧 [Operasyonel İşler](./operasyonel-isler/README.md)
Günlük operasyonu (misafir yorumları, geri bildirim, iç raporlama) otomatikleştiren sistemler.

### 📊 Marketing
- [Raporlama](./marketing/raporlama/README.md) — Performans verisini toplayıp rapor/dashboard haline getiren otomasyonlar
- [İstihbarat](./marketing/istihbarat/README.md) — Rakip ve pazar verisini otomatik toplayan sistemler
- [Kontrol](./marketing/kontrol/README.md) — SEO/Ads sağlık kontrolü ve uyarı sistemleri

### 🚀 [Business Development / Growth](./business-development-growth/README.md)
Müşteri iletişimi ve büyüme kanallarını otomatikleştiren sistemler.

---

## Kullanılan Teknolojiler

`n8n` · `Supabase` · `Google Ads API` · `Google Analytics / Search Console` · `Semrush` · `SerpAPI` · `DataForSEO` · `OpenAI / Anthropic Claude (LLM Agent'lar)` · `Meta Ads API` · `WhatsApp / Instagram Business API` · `ElevenLabs` · `Google Sheets / Drive` · `Docker + APScheduler (VPS)` · `Windows Task Scheduler` · `Python` · `Node.js`

Her otomasyon için: **ne işe yarıyor, tetikleyicisi, kullandığı entegrasyonlar, akış özeti ve aktif/pasif durumu** ilgili kategori sayfasında listelenmiştir.
