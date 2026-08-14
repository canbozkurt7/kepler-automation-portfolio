[← Ana sayfa](../README.md)

# 🚀 Business Development / Growth

Müşteri iletişimi ve büyüme kanallarını otomatikleştiren sistemler.

---

## Instagram DM Replier

**Ne işe yarıyor:** Kepler Club'ın Instagram hesabına gelen direkt mesajları otomatik karşılayıp bir AI Agent aracılığıyla, işletmeye özel bilgi tabanından (fiyatlar, hizmetler, SSS) yanıt üreten bir müşteri hizmetleri chatbot'u.

**Tetikleyici:** Webhook — Instagram'a yeni mesaj geldiğinde otomatik tetiklenir.

**Kullanılan araçlar/entegrasyonlar:** Instagram Messaging API, AI Agent (Anthropic Claude Haiku), vektör tabanlı bilgi tabanı (Supabase), Postgres tabanlı sohbet hafızası.

**Akış özeti:**
- Gelen mesaj boş değilse AI Agent'a iletilir.
- Agent, işletmeye özel bilgi tabanından (hangi lokasyona ait olduğu anlaşılarak) ilgili bilgiyi arayıp yanıt üretir; kayıp eşya, rezervasyon bilgisi ekranı, kapsül oda görseli gibi özel durumlar için önceden tanımlı standart yanıtlar var.
- Kullanıcı bazlı konuşma geçmişi hafızada tutulur.
- Yanıt Instagram DM olarak geri gönderilir.

**Durum:** Pasif.

---

## Kepler Club Mailing

**Ne işe yarıyor:** Yeni bir mailing/e-posta pazarlama entegrasyonunun (Resend üzerinden) ilk kurulum adımı — yeni kişi (contact) oluşturulduğunda tetiklenecek şekilde tasarlanmış, henüz geliştirme/kurulum aşamasında bir otomasyon.

**Tetikleyici:** Yeni kişi oluşturma olayı (Resend) + manuel test tetikleyicisi.

**Kullanılan araçlar/entegrasyonlar:** Resend (e-posta gönderim platformu).

**Akış özeti:**
- Şu an yalnızca tetikleyici node'lar tanımlı; asıl e-posta içeriği/akış mantığı henüz eklenmemiş.

**Durum:** Pasif, kurulum aşamasında.

---

## ElevenLabs AI Assistant

**Ne işe yarıyor:** Sesli AI asistan — misafir/müşteri sorularını sesli olarak yanıtlayan bir konuşma agent'ı.

**Tetikleyici:** Talep üzerine (sesli arama/konuşma başlatıldığında).

**Kullanılan araçlar/entegrasyonlar:** ElevenLabs Agents platformu.

**Durum:** Kuruldu; entegrasyon/erişim ayarları üzerinde çalışılıyor.
