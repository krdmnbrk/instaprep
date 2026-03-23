# 📷 InstaPrep — Instagram Fotoğraf Hazırlama Aracı

Fotoğraflarınıza EXIF bilgilerini içeren şık overlay'lar ekleyin, before/after karşılaştırmaları oluşturun ve Instagram'a hazır görseller dışa aktarın — tamamen tarayıcı içinde çalışan, sunucu gerektirmeyen tek sayfalık uygulama.

🔗 **[Canlı Demo](https://krdmnbrk.github.io/instaprep/)**

---

## ✨ Özellikler

### 🖼 EXIF Overlay
- Fotoğraftan EXIF verilerini otomatik okuma (kamera, lens, ISO, enstantane, diyafram)
- **Parametrik metin şablonu** — `{camera}`, `{lens}`, `{iso}`, `{shutterSpeed}`, `{aperture}` yer tutucularıyla tam özelleştirme
- Boş alanlar ve artık ayırıcılar otomatik temizlenir
- EXIF bulunamazsa alanları manuel düzenleme imkanı
- Glassmorphism tarzı overlay kutusu (bulanıklık + yarı saydam arka plan)
- Tam kontrol: font ailesi, boyut, renk, arka plan rengi/opaklığı, blur, köşe yuvarlaklığı, padding, dikey konum

### ↔️ Before / After
- Editlenmemiş ve editlenmiş fotoğraf yan yana karşılaştırma
- Ayarlanabilir split oranı
- Özelleştirilebilir ayırıcı çizgi (renk, kalınlık)
- **Tamamen parametrik etiketler** — metin, font, boyut, renk, arka plan, blur, köşe yuvarlaklığı, padding, dikey konum
- Etiketlerde glassmorphism efekti desteği

### 🎨 Kırpma & Dışa Aktarma
- Aspect ratio seçenekleri: Orijinal, 1:1, 4:5, 16:9
- JPEG veya PNG formatında dışa aktarma
- JPEG kalite kontrolü (%50–100)

### 💾 Preset Sistemi
- Tüm ayarları preset olarak **localStorage'a kaydetme**
- Preset listesinden tek tıkla uygulama
- Presetleri **JSON dosyası olarak indirme**
- JSON dosyasından **preset içe aktarma** — cihazlar arası taşınabilirlik
- Presetleri silme

### 🧠 Akıllı EXIF Okuma
- Geniş kapsamlı EXIF segmentlerini tarama (TIFF, EXIF, XMP, IPTC)
- Başarısız olursa fallback stratejisi
- Bilgilendirici hata mesajları (kırmızı: hata, turuncu: veri bulunamadı)
- EXIF olmayan görsellerde sorunsuz manuel giriş

---

## 🛠 Teknolojiler

| Teknoloji | Kullanım |
|-----------|----------|
| React 18 | UI bileşen yapısı (CDN üzerinden) |
| Babel Standalone | JSX derleme (tarayıcı içi) |
| exifr | EXIF metadata okuma |
| Canvas API | Gerçek zamanlı görsel render ve dışa aktarma |
| localStorage | Ayar ve preset kalıcılığı |

---

## 🚀 Kullanım

Herhangi bir kurulum veya build adımı gerekmez. Sadece `index.html` dosyasını bir tarayıcıda açın veya [canlı demo](https://krdmnbrk.github.io/instaprep/) linkini kullanın.

1. **Editlenmemiş fotoğrafı** yükleyin (EXIF otomatik okunur)
2. **Editlenmiş fotoğrafı** yükleyin (Before/After için)
3. Sekme seçin: **EXIF Overlay** veya **Before / After**
4. Ayarları düzenleyin, sonucu önizleyin
5. **İndir** butonuyla kaydedin

---

## 📁 Proje Yapısı

```
instaprep/
└── index.html    # Tek dosya — tüm HTML, CSS ve JavaScript
```

---

## 📄 Lisans

MIT
