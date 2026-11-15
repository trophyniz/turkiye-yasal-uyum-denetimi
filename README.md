# Türkiye Yasal Uyum Denetim Skilli

**Mobil uygulama, web sitesi ve masaüstü yazılımları Türk hukuku açısından denetleyen hazır AI skill’i.**

Türkiye’de ürün çıkaran geliştiriciler, ajanslar ve ürün ekipleri için tasarlandı. En sık karşılaşılan (ve en pahalıya patlayan) uyum açıklarını, ceza yemeden önce yakalamana yardımcı olur.

---

## Neden bu skill var?

Türkiye’de aktif olarak denetlenen konular:

- **KVKK** (kişisel veri)
- **6502 sayılı Kanun** (tüketici koruma & abonelik)
- **6563 sayılı Kanun** (ticari e-posta)
- **5651 sayılı Kanun** (yer sağlayıcı yükümlülükleri)
- **5846 sayılı Kanun** (telif / kullanıcı içeriği)
- Çerez kuralları, mesafeli satış yükümlülükleri ve AI içerik şeffaflığı

Çoğu AI asistanı genel GDPR bilgisine sahip olsa da, Türkçe’ye özgü kuralları, ceza tutarlarını ve pratik kırmızı bayrakları sistematik kontrol etmez. Bu skill tam olarak bunu yapar.

---

## Ne kontrol eder? (10 alan)

| # | Alan | Ana Kanun |
|---|------|----------|
| 1 | Ödeme ekranı ve otomatik yenileme | 6502 |
| 2 | Ticari / tanıtım e-postaları | 6563 |
| 3 | Kullanıcı yüklediği telifli içerik | 5846 |
| 4 | Yer sağlayıcı bildirimi ve kaldırma | 5651 |
| 5 | Aydınlatma metni | KVKK m.10 |
| 6 | Yurt dışı veri aktarımı ve harici SDK’lar | KVKK m.9 ve m.12 |
| 7 | Çerez onayı ve tercih merkezi | KVKK Çerez Rehberi |
| 8 | Mesafeli satış / ön bilgilendirme | 6502 + Yönetmelik |
| 9 | AI üretimi ticari içerik etiketleme | Reklam Yönetmeliği |
| 10 | Operasyonel noktalar (VERBİS, log, mağaza etiketleri) | Karışık |

Her bulgu **dosya yolu + satır numarası** ile raporlanır. Skill asla uydurma bulgu üretmez ve sen açıkça istemeden hiçbir kodu değiştirmez.

---

## Nasıl kullanılır?

1. Skill klasörünü ajanının skills dizinine koy.
2. Herhangi bir projeyi aç (web, mobil, masaüstü).
3. Şunlardan birini söyle:

```
Bu projeyi Türkiye yasal uyum açısından denetle
```

```
KVKK + 6502 + 5651 kontrolü yap
```

```
turkiye-yasal-uyum-denetimi skill’ini kullan ve rapor üret
```

Skill şunları yapar:
- Kod tabanını inceler
- Yapılandırılmış tablo üretir
- En riskli 5 maddeyi sıralar
- Herhangi bir kod yazmadan önce hangi maddeleri düzeltmek istediğini sorar

---

## Örnek çıktı (kısaltılmış)

```
| Başlık                         | Durum    | Bulgu                             | Risk   |
|--------------------------------|----------|-----------------------------------|--------|
| 1. Ödeme ve Abonelik           | Kısmen   | lib/screens/paywall.dart:142      | Yüksek |
| 5. Aydınlatma Metni            | Yok      | Aydınlatma metni bulunamadı       | Yüksek |
| 6. Yurt Dışı Veri              | Var      | Google Fonts + Mixpanel           | Yüksek |
| 7. Çerez Onayı                 | Yok      | Banner veya tercih merkezi yok    | Yüksek |
| 4. Yer Sağlayıcı               | Yok      | 5651 bildirimi görünmüyor         | Orta   |

En önemli 5 risk:
1. Eksik aydınlatma metni (KVKK m.10) – 1,7 milyon TL’ye kadar
2. Google Fonts + analitik, aktarım dayanağı belirsiz
3. Otomatik yenileme şartları net gösterilmemiş
4. Çerez onay mekanizması yok
5. Yer sağlayıcı iletişim bildirimi yok
```

(Tam şablon için `assets/rapor-sablonu.md` dosyasına bak.)

---

## Tasarım prensipleri

- **Kanıta dayalı** — her iddia dosya:satır ile desteklenir
- **Temkinli** — “doğrulanamadı” demek, tahmin etmekten iyidir
- **Yıkıcı değil** — sen onaylamadan hiçbir kod değiştirilmez
- **Dürüst** — her zaman “Bu hukuki tavsiye değildir” uyarısıyla biter

---

## Önemli uyarı

Bu skill bir **teknik denetim yardımcısıdır**, Türk avukatının yerini tutmaz.  
Ceza tutarları ve uygulama pratikleri değişebilir. Üretim kararlarında mutlaka nitelikli bir avukata danış.

---

## Lisans

MIT License — özgürce kullanabilir, değiştirebilir ve dağıtabilirsin.  
Detay için `LICENSE` dosyasına bak.

---

## Katkı

İyileştirme, ek kontrol listeleri ve daha iyi örnekler memnuniyetle karşılanır.  
Issue veya pull request açabilirsin.
