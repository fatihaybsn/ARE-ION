# ARE-ION
# C# Yer Kontrol İstasyonu (Teknofest Savaşan İHA 2025 GCS)

C# ve MAVLink kütüphanesi kullanılarak Teknofest 2025 Savaşan İHA yarışması kapsamında geliştirilmiş, kapsamlı bir **Yer Kontrol İstasyonu (Ground Control Station - GCS)** yazılımıdır.  
Pixhawk **Orange Cube** uçuş bilgisayarına **telemetri** (Seri/UDP/TCP) üzerinden bağlanır; İHA’dan **irtifa, hız, yaw, GPS** gibi verileri canlı alır ve **harita** üzerinde hem anlık konumu hem de **yasaklı alanları (geofence)** gösterir.

> **Durum:** Aktif geliştirme • **Hedef platform:** Windows (.NET)

---
<img width="1919" height="1079" alt="Ekran görüntüsü 2025-10-10 193808" src="https://github.com/user-attachments/assets/6ff9124a-67d4-46d6-8ca2-de2da2909c6c" />

ARE-ION, operatörün hava aracına tam hakimiyet kurmasını sağlayan hibrit bir mimariye sahiptir. Arayüz ve ana kontrol mantığı C# (.NET 8.0 WinForms) üzerinde çalışırken, görüntü işleme ve ağ tabanlı video aktarım modülleri performans avantajı nedeniyle Python ile geliştirilmiş ve sisteme entegre edilmiştir.

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

## Özellikler ve Kullanım

### 1. Bağlantı Modülü
**Port Seçimi:** Bilgisayara bağlı telemetri modülünün (RFD900, LoRa vb.) COM portu otomatik listelenir.
**Baud Rate:** Varsayılan 57600 veya 115200 seçenekleri.
**Bağlan/Kes:** Bağlantı durumunu gösteren görsel indikatörler.

### 2. Kokpit ve Göstergeler
**Yapay Ufuk (HUD):** Pitch ve Roll hareketlerinin görsel temsili.
**Hız ve İrtifa:** Anlık yer hızı (m/s) ve barometrik/GPS irtifası.
**Mod Göstergesi:** (STABILIZE, LOITER, AUTO, GUIDED vb.)

### 3. Harita ve Görev
Harita üzerinde İHA ikonu, burnunun baktığı yöne (Heading) göre döner.
Yasaklı alanlar kırmızı poligonlar ile çizilir.
İHA yasaklı alana girerse sistem sesli ve görsel uyarı verir.

### 4. Video Akışı
"Görüntü Başlat" butonu TCP_goruntu_aktarim_win.exe servisini tetikler.
Görüntü penceresi üzerinden hedef tespiti veya FPV sürüş yapılabilir.

## Kurulum

### Gereksinimler
- **.NET SDK** 6.0+ (veya kullandığın sürüm)
- **Visual Studio 2022** (Community/Pro) ya da JetBrains Rider
- Pixhawk **Orange Cube** (ArduPilot/PX4), telemetri modülü veya UDP bridge
- NuGet bağımlılıkları (MAVLink, harita bileşeni vb.)

### Adımlar
- Projeyi klonlayın veya indirin.
- ARES_Fatih_AYIBASAN.sln dosyasını Visual Studio ile açın.
- NuGet Paketlerini Geri Yükle (Restore NuGet Packages) seçeneği ile bağımlılıkları (Asv.Mavlink, WebView2 vb.) yükleyin.
- Projeyi Debug veya Release modunda derleyin (Ctrl + Shift + B).
- Uygulamanın çalışacağı dizinde (bin/Debug/net8.0-windows/) api.exe ve TCP_goruntu_aktarim_win.exe dosyalarının bulunduğundan emin olun. (Bu dosyalar ana uygulamanın çalışması için kritiktir).
- Start tuşuna basarak uygulamayı başlatın.

### NOT
Bu yazılım, yarışma kuralları ve güvenlik protokolleri çerçevesinde test edilmelidir. Yasaklı alan ihlalleri veya bağlantı kopması durumunda devreye girecek otonom prosedürler (Failsafe) uçuş kontrolcüsü (Pixhawk/Cube) üzerinden ayrıca yapılandırılmalıdır.

### Ekstra Bilgiler

* **Geliştirici**: [Fatih AYIBASAN] (Bilgisayar Mühendisliği Öğrencisi)
* **E-posta**: [fathaybasn@gmail.com]

---
