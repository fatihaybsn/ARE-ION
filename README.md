# ARE-ION
# ARES – C# Yer Kontrol İstasyonu (Teknofest Savaşan İHA)

C# ve MAVLink kütüphanesi kullanılarak geliştirilen **Yer Kontrol İstasyonu (GCS)**.  
Pixhawk **Orange Cube** uçuş bilgisayarına **telemetri** (Seri/UDP/TCP) üzerinden bağlanır; İHA’dan **irtifa, hız, yaw, GPS** gibi verileri canlı alır ve **harita** üzerinde hem anlık konumu hem de **yasaklı alanları (geofence)** gösterir.

> **Durum:** Aktif geliştirme • **Hedef platform:** Windows (.NET)

## İçindekiler
- [Özellikler](#özellikler)
- [Mimari ve Teknolojiler](#mimari-ve-teknolojiler)
- [Kurulum](#kurulum)
- [Hızlı Başlangıç](#hızlı-başlangıç)
- [Bağlantı & Telemetri](#bağlantı--telemetri)
- [Harita & Geofence](#harita--geofence)
- [Proje Yapısı](#proje-yapısı)
- [Yapılandırma (appsettings.json - opsiyonel)](#yapılandırma-appsettingsjson---opsiyonel)
- [Sıkça Sorulanlar](#sıkça-sorulanlar)
- [Yol Haritası](#yol-haritası)
- [Katkı](#katkı)
- [Lisans](#lisans)
- [Teşekkür](#teşekkür)
- [English Summary](#english-summary)

---
<img width="1919" height="1079" alt="Ekran görüntüsü 2025-10-10 193808" src="https://github.com/user-attachments/assets/6ff9124a-67d4-46d6-8ca2-de2da2909c6c" />

## Özellikler
- **MAVLink** üzerinden Pixhawk Orange Cube’a bağlantı (Seri/UDP/TCP).
- Canlı **telemetri akışı:** irtifa, anlık hız, yaw/heading, GPS koordinatları, uçuş modu vb.
- **Harita entegrasyonu:** İHA canlı konumu, takip izi (track), yakınlaştırma/taşıma.
- **Yasaklı Alan (Geofence):** yarışma kurallarına uygun daire/çokgen alan tanımı ve harita üstünde görselleştirme.
- Basit arayüz: **port/baud** seçimi, **bağlan/ayır**, bağlantı durumu ve takım numarası gösterimi.
- Genişletilebilir yapı: Görev planlama (waypoint), log kayıt/oynatma, çoklu araç desteği için hazır katmanlar.

## Mimari ve Teknolojiler
- **.NET / C#** (WinForms veya WPF – projeye göre)
- **MAVLink .NET** (NuGet)
- **Harita**: GMap.NET veya WebView + Leaflet/OpenStreetMap (projendeki seçime göre)
- **İletişim**: SerialPort, UDP, TCP soketleri
- **Katmanlı yapı**: Core (telemetri & MAVLink), UI (GCS arayüzü), Map (harita bileşeni)

> Not: Kullandığın MAVLink ve harita paketlerinin **gerçek NuGet paket adlarını** bu bölüme ekleyebilirsin.

---

## Kurulum

### Gereksinimler
- **.NET SDK** 6.0+ (veya kullandığın sürüm)
- **Visual Studio 2022** (Community/Pro) ya da JetBrains Rider
- Pixhawk **Orange Cube** (ArduPilot/PX4), telemetri modülü veya UDP bridge
- NuGet bağımlılıkları (MAVLink, harita bileşeni vb.)

### Repoyu Klonla
```bash
git clone https://github.com/<kullanici-adi>/<repo-adi>.git
cd <repo-adi>

<img width="1919" height="1079" alt="Ekran görüntüsü 2025-10-10 193808" src="https://github.com/user-attachments/assets/93e5bb2e-ca02-46ae-8d51-9b503fbb823c" />
