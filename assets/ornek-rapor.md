# Türkiye Yasal Uyum Denetim Raporu
**Örnek Çıktı**

**Proje:** Demo SaaS Web Uygulaması (Next.js + Stripe)  
**Tarih:** 2026-11-15  
**Denetçi:** turkiye-yasal-uyum-denetimi skill  
**Uyarı:** Bu rapor hukuki tavsiye niteliği taşımaz. Nihai değerlendirme için mutlaka nitelikli bir Türk avukatına danışın. Tutarlar 2026 yılına aittir ve değişebilir.

## Proje Özeti

- **Platform:** Web (Next.js 14, React)
- **Kullanılan hizmetler:** Stripe (ödeme), Resend (e-posta), Mixpanel (analitik), Sentry (hata izleme), Google Fonts
- **Tespit edilen kişisel veriler:** e-posta, ad, IP adresi, cihaz/tarayıcı bilgisi, ödeme yöntemi token’ları, kullanım olayları

## Denetim Tablosu

| Başlık | Durum | Bulgu (dosya:satır) | Risk | Önerilen düzeltme |
|--------|-------|---------------------|------|-------------------|
| 1. Ödeme ve Abonelik (6502) | Kısmen | `app/pricing/page.tsx:87-112` – fiyat görünüyor ama otomatik yenileme ve iptal yöntemi sadece Kullanım Koşulları linkinde | Yüksek | Ödeme butonundan önce aynı sayfada yenileme periyodu, otomatik yenileme ve iptal yöntemini açıkça göster |
| 2. Ticari E-posta (6563) | Kısmen | `lib/email/templates/welcome.tsx:24` – gönderen adı var, çıkış linki var ama çalışmayan bir route’a gidiyor | Orta | Çıkış (unsubscribe) endpoint’ini çalışır hale getir ve opt-out’u kaydet |
| 3. Kullanıcı Telifli İçerik (5846) | Yok | Kullanıcı yükleme özelliği tespit edilmedi | — | Geçerli değil |
| 4. Yer Sağlayıcı (5651) | Yok | Arayüzde veya footer’da yer sağlayıcı bildirimi / iletişim bilgisi yok | Orta | “Yer Sağlayıcı Bilgileri” bölümü ekle (unvan, adres, e-posta) |
| 5. Aydınlatma Metni (KVKK m.10) | Kısmen | `app/privacy/page.tsx` var ama Mixpanel, Sentry ve verinin yurt dışına çıktığı belirtilmemiş | Yüksek | Tüm işleyenleri, amaçları, saklama sürelerini ve yurt dışı aktarım dayanağını ekle |
| 6. Yurt Dışı Veri (KVKK m.9/m.12) | Var | `layout.tsx:18` Google Fonts CDN; `lib/analytics.ts:9` Mixpanel; `sentry.client.config.ts` – hepsi IP + cihaz verisini Türkiye dışına gönderiyor | Yüksek | Aktarım dayanağını aydınlatma metninde belirt, fontları mümkünse self-host et |
| 7. Çerez Onayı | Yok | Çerez banner’ı veya tercih merkezi bulunamadı | Yüksek | Zorunlu olmayan çerezleri (Mixpanel) kullanıcı kabul/reddetmeden önce engelleyen bir banner ekle |
| 8. Mesafeli Satış / Ön Bilgilendirme | Kısmen | Kullanım Koşulları linki var ama ödeme öncesi ayrı bir ön bilgilendirme sayfası yok | Orta | Ödeme sayfasında fiyat, süre ve cayma hakkı özetini net göster |
| 9. AI İçerik Şeffaflığı | Doğrulanamadı | Mevcut kodda belirgin AI üretimi ticari içerik tespit edilmedi | Düşük | Pazarlama metinlerinde üretken AI kullanılmaya başlanırsa etiketlemeyi takip et |
| 10. Operasyonel noktalar | Kısmen | VERBİS’ten bahsedilmiyor; trafik log saklama kararı yok; mağaza etiketleri web olduğu için geçerli değil | Orta | VERBİS durumunu hukuk danışmanıyla netleştir, log saklama süresine karar ver |

## En Önemli 5 Risk (Öncelik Sırasına Göre)

1. **Eksik / yetersiz aydınlatma metni + yurt dışı aktarımlar** (Başlık 5 ve 6)  
   KVKK açısından en pratik risk. m.18 kapsamında ~1,7 milyon TL’ye kadar + Kurul’un güvenlik uygulamaları.

2. **Çerez onay mekanizması yok** (Başlık 7)  
   Çok sık denetlenen konu. Zorunlu olmayan çerezler (Mixpanel) şu anda onaysız yükleniyor.

3. **Abonelik yenileme şartları ödeme ekranında net değil** (Başlık 1)  
   Klasik 6502 / haksız ticari uygulama riski. Bilerek gizleme kabul edilirse çok yüksek cezalara çıkabilir.

4. **Yer sağlayıcı bildirimi yok** (Başlık 4)  
   5651’in açık yükümlülüğü. Kolay düzeltilir ama hâlâ sık eksik kalıyor.

5. **Ticari e-postalarda çalışmayan çıkış linki** (Başlık 2)  
   Doğrudan 6563 ihlali. Yetkililerin test etmesi kolay, ceza tutarı anlamlı.

## Sonraki Adım

Yukarıdaki bulgulardan hangilerini düzeltmemi istersiniz?  
Onayınızı almadan hiçbir kod yazmayacağım veya değiştirmeyeceğim.
