# CLAUDE.md — InstaPrep Proje Özeti

## Proje Nedir?

**InstaPrep**, fotoğrafları Instagram'a paylaşıma hazırlamak için tasarlanmış, tamamen tarayıcı içinde çalışan tek sayfalık (single-file) bir web uygulamasıdır. Sunucu gerektirmez; tüm işlemler istemci tarafında yapılır.

**Canlı Demo:** https://krdmnbrk.github.io/instaprep/
**Repo:** https://github.com/krdmnbrk/instaprep

## Teknik Mimari

- **Tek dosya:** `index.html` (~2558 satır) — HTML, CSS ve JSX tek dosyada
- **React 18** (UMD, CDN üzerinden) + **Babel Standalone** (tarayıcıda JSX derleme)
- **exifr** kütüphanesi (CDN) — EXIF metadata okuma
- **Canvas API** — tüm görsel render ve dışa aktarma işlemleri
- **useReducer** ile state yönetimi
- **localStorage** ile ayar ve preset kalıcılığı
- **i18n:** Türkçe (tr) ve İngilizce (en) çeviriler inline tanımlı
- **Tema:** Dark / Light mod (CSS değişkenleri + `data-theme` attribute)

## Dosya Yapısı

```
instaprep/
├── index.html     # Tüm uygulama (HTML + CSS + JSX)
├── README.md      # Proje dokümantasyonu
└── CLAUDE.md      # Bu dosya — AI asistan için proje özeti
```

## Temel Özellikler

### 1. EXIF Overlay
- Fotoğraftan EXIF otomatik okunur: kamera, lens, ISO, enstantane, diyafram, odak uzaklığı, tarih
- Parametrik metin şablonu: `{camera}`, `{lens}`, `{iso}`, `{shutterSpeed}`, `{aperture}`, `{focalLength}`, `{date}`, `{custom}`
- Glassmorphism tarzı overlay kutusu (blur + yarı saydam bg)
- Tam kontrol: font, boyut, renk, bg rengi/opaklık, blur, köşe yuvarlaklığı, padding, dikey/yatay konum
- Overlay göster/gizle toggle
- Özel metin alanı (kullanıcı adı, lokasyon vb.)

### 2. Before / After
- Editlenmemiş ve editlenmiş fotoğraf karşılaştırma
- 8 yön desteği: soldan-sağa, sağdan-sola, yukarıdan-aşağıya, aşağıdan-yukarıya, 4 çapraz yön
- Ayarlanabilir split oranı, özelleştirilebilir ayırıcı çizgi
- Parametrik etiketler (glassmorphism efektli)

### 3. Çerçeve (Frame)
- Fotoğraf etrafına özelleştirilebilir çerçeve ekleme
- Çerçeve rengi ve kalınlığı ayarlanabilir

### 4. Kırpma & Dışa Aktarma
- Aspect ratio: Orijinal, 1:1, 4:5, 16:9, 9:16
- JPEG/PNG format seçimi, JPEG kalite kontrolü
- **Instagram Optimize** modu: genişlik 1080px, JPEG %92
- Dosya boyutu önizleme
- Panoya kopyalama (clipboard)

### 5. Preset & Template Sistemi
- Tüm ayarları preset olarak kaydetme/yükleme
- Yatay/dikey fotoğraflar için ayrı template desteği
- JSON olarak dışa/içe aktarma

### 6. Diğer
- Dark/Light tema
- TR/EN dil desteği
- Slider'larda çift tıklama ile varsayılana dönme

## Kod Yapısı (index.html içindeki bölümler)

| Satır Aralığı (yaklaşık) | İçerik |
|---------------------------|--------|
| 1–11 | Head, CDN bağlantıları |
| 12–670 | CSS stilleri (dark/light tema, responsive) |
| 676–680 | React imports, context tanımları |
| 680–870 | Çeviriler (TR + EN) |
| 870–930 | localStorage yardımcıları, `defaultSettings` |
| 930–1010 | `initialState`, `ASPECT_RATIOS`, `pageDefaults` |
| 1010–1130 | Reducer fonksiyonu (tüm action'lar) |
| 1130–1200 | `parseExif` fonksiyonu (EXIF metadata çıkarma) |
| 1200–1230 | `getCropRect`, `roundRect` yardımcı fonksiyonlar |
| 1230–1290 | `Accordion`, `ExifDisplay` bileşenleri |
| 1290–1350 | `SettingsPanel` — Kırpma, Çerçeve |
| 1350–1500 | `SettingsPanel` — Overlay ayarları |
| 1500–1670 | `SettingsPanel` — Before/After, Export ayarları |
| 1670–1780 | `PresetPanel` bileşeni |
| 1780–2200 | `CanvasPreview` — Canvas render (overlay + before/after) |
| 2200–2420 | `App` bileşeni — dosya yükleme, download, clipboard, state |
| 2420–2560 | `App` JSX return — sidebar, tabs, canvas, butonlar |

## State Yapısı

```js
{
  activeTab: 'overlay' | 'beforeafter',
  editedImage: HTMLImageElement | null,
  uneditedImage: HTMLImageElement | null,
  editedFile: File | null,
  uneditedFile: File | null,
  exif: { camera, lens, iso, shutterSpeed, aperture, focalLength, dateTime, custom },
  overlay: { fontFamily, fontSize, fontColor, bgColor, bgOpacity, blur, borderRadius, verticalPosition, horizontalPosition, padding, showOverlay, textTemplate },
  frame: { enabled, color, size },
  beforeAfter: { direction, splitRatio, showDivider, dividerColor, dividerWidth, showLabels, beforeLabel, afterLabel, ... },
  exportSettings: { format, jpegQuality, aspectRatio, resizeMode },
  notification: null | { key, message, name }
}
```

## Geliştirme Notları

- Herhangi bir build sistemi yok — `index.html` doğrudan tarayıcıda açılır
- Babel Standalone tarayıcıda JSX derler, production build için ayrı bir süreç yok
- Tüm görseller Canvas API ile render edilir, DOM'a img olarak eklenmez
- EXIF okuma `exifr` kütüphanesi ile yapılır, başarısız olursa fallback dener
- Settings her değişiklikte localStorage'a otomatik kaydedilir
