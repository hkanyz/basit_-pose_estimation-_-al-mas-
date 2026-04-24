# 🎮 AI Pose Game — Vücut Hareketleriyle Oyun

Yapay zeka destekli, kamera üzerinden vücut hareketlerini algılayarak oynanan açık kaynak kodlu bir tarayıcı oyunu.

**Google MediaPipe Pose** modeli kullanılarak oyuncunun el ve ayak pozisyonları gerçek zamanlı olarak okunur ve oyun mekaniğine dönüştürülür. Herhangi bir kurulum veya indirme gerektirmeden, tarayıcı üzerinden doğrudan oynanabilir.

---

## 🚀 Özellikler

| Özellik | Detay |
|---|---|
| **AI Vücut Algılama** | MediaPipe Pose ile 33 vücut noktası gerçek zamanlı takip |
| **El ile Etkileşim** | Düşen dairelere sadece ellerle dokunarak puan kazanma |
| **Kamera Görüntüsü** | Oyuncu kendini ekranda canlı olarak görür |
| **Dinamik Zorluk** | Her 30 puanda ekrandaki top sayısı 2 katına çıkar (maks. 48) |
| **Puan Sistemi** | Mavi daire = +2, Kırmızı daire = -1 |
| **Responsive Tasarım** | Top boyutları ve hızları ekran oranına göre otomatik ayarlanır |
| **Sıfır Kurulum** | Tarayıcıyı aç, kameraya izin ver, oyna |

---

## 🎯 Oyun Mekaniği

1. Ekranda her zaman **6 adet top** bulunur (başlangıç).
2. **Mavi toplara** ellerinizle dokunun → **+2 puan** kazanın.
3. **Kırmızı toplardan** kaçının → Dokunursanız **-1 puan** kaybedersiniz.
4. Her **30 puanda** ekrandaki top sayısı **2 katına** çıkar:
   - `0–29 puan → 6 top`
   - `30–59 puan → 12 top`
   - `60–89 puan → 24 top`
   - `90+ puan → 48 top (maksimum)`
5. Ulaşılan zorluk seviyesi **asla geri düşmez**.

---

## 🛠️ Teknoloji Yığını

| Katman | Teknoloji |
|---|---|
| **Yapay Zeka** | [Google MediaPipe Tasks Vision](https://ai.google.dev/edge/mediapipe/solutions/vision/pose_landmarker) (Apache 2.0) |
| **Frontend** | Vanilla JavaScript, HTML5 Canvas |
| **Bundler** | [Vite](https://vitejs.dev/) |
| **Stil** | Vanilla CSS (Dark Mode, Glassmorphism) |
| **Font** | [Outfit](https://fonts.google.com/specimen/Outfit) (Google Fonts) |

---

## 📁 Proje Yapısı

```
aigame/
├── index.html              # Ana HTML şablonu (video, canvas, puan kutusu)
├── style.css               # Arayüz stilleri (dark mode, glassmorphism)
├── package.json            # Proje bağımlılıkları
└── src/
    ├── main.js             # Kamera erişimi, MediaPipe model yükleme, oyun döngüsü
    ├── game.js             # Oyun motoru (düşen daireler, çarpışma, puan, render)
    └── poseAnalyzer.js     # Vücut pozisyon analizi (el/ayak konum komutları)
```

---

## ⚡ Kurulum ve Çalıştırma

### Gereksinimler
- [Node.js](https://nodejs.org/) (v18+)
- Kameralı bir bilgisayar
- Modern bir tarayıcı (Chrome, Edge, Firefox)


## 🧠 Nasıl Çalışır?

```
Kamera Akışı (getUserMedia)
        │
        ▼
  MediaPipe Pose Modeli (WebAssembly + WebGL)
        │
        ▼
  33 Vücut Noktası (Landmarks)
        │
        ├──▶ poseAnalyzer.js  →  "Sağ el başın üstünde mi?" gibi mantık kontrolleri
        │
        └──▶ game.js  →  El koordinatları ile düşen daire çarpışma tespiti
                │
                ▼
        HTML5 Canvas Render (kamera + toplar + puan)
```

### Algılanan Vücut Noktaları (Örnekler)

| Index | Nokta | Kullanım |
|---|---|---|
| 0 | Burun | Referans noktası (baş seviyesi) |
| 15 | Sol Bilek | Sol el çarpışma tespiti |
| 16 | Sağ Bilek | Sağ el çarpışma tespiti |
| 19 | Sol İşaret Parmağı | Sol el hassas temas |
| 20 | Sağ İşaret Parmağı | Sağ el hassas temas |
| 27 | Sol Ayak Bileği | Gelecek: ayak ile etkileşim |
| 28 | Sağ Ayak Bileği | Gelecek: ayak ile etkileşim |

---

## 📜 Lisans

Bu proje **açık kaynak kodludur** ve ticari kullanıma uygundur.

- Proje Kodu: **MIT License**
- MediaPipe: **Apache 2.0 License**

---

## 🔮 Yol Haritası

- [ ] Çok oyunculu mod (WebSocket / PeerJS ile LAN/Online)
- [ ] Bluetooth dış donanım desteği (Web Bluetooth API)
- [ ] Ayak ile etkileşim modu
- [ ] Ses efektleri ve müzik
- [ ] Seviye sistemi ve oyun sonu ekranı
- [ ] Mobil tarayıcı uyumluluğu

---

## 🤝 Katkıda Bulunma

1. Bu depoyu forklayın
2. Yeni bir dal oluşturun (`git checkout -b ozellik/yeni-ozellik`)
3. Değişikliklerinizi commit edin (`git commit -m "Yeni özellik eklendi"`)
4. Dalınıza push edin (`git push origin ozellik/yeni-ozellik`)
5. Pull Request açın

---

> **Not:** Bu proje Google MediaPipe'ın açık kaynak yapay zeka modellerini kullanmaktadır. Herhangi bir sunucu tarafı işlem gerektirmez — tüm AI hesaplamaları kullanıcının tarayıcısında yerel olarak çalışır.
