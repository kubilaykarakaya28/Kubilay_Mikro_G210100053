# Kubilay_Mikro_G210100053
İleri mikro ödevi G210100053 
<img width="546" height="515" alt="image" src="https://github.com/user-attachments/assets/371723c4-5ff2-4837-b588-fe7c92df2f99" />

Tiva C & C# PC Arayüzü ile Tam Çift Yönlü Haberleşme Sistemi
Bu proje, Tiva C Series (TM4C123GH6PM) mikrodenetleyicisi ile C# (Windows Forms) tabanlı bir masaüstü yazılımı arasında UART (Seri Haberleşme) protokolü kullanılarak gerçek zamanlı ve karşılıklı veri transferini gerçekleştirmek amacıyla geliştirilmiştir.

🎯 Projenin Amacı
Gömülü sistemler ile masaüstü yazılımları arasında güvenli, senkron ve veri kaybı olmadan çalışan bir haberleşme protokolü tasarlamak; sensör verilerini izlerken aynı anda sistemi uzaktan kontrol edebilmektir.

🚀 Temel Özellikler
1. PC'den Mikrodenetleyiciye Kontrol (Arayüz -> Tiva C)
Zaman Senkronizasyonu: C# arayüzü, bilgisayarın anlık sistem saatini (DateTime.Now) okur ve Tiva C'ye gönderir. Tiva C, dahili zamanlayıcısını bu veriye göre günceller.

Metin Gönderimi: Kullanıcı arayüzünden girilen metinler, Tiva C'ye bağlı LCD ekran (16x2) üzerinde anlık olarak görüntülenir.

2. Mikrodenetleyiciden PC'ye Veri Akışı (Tiva C -> Arayüz)
Analog Veri Okuma (ADC): PE3 pinine bağlı analog sensör/potansiyometre verisi (12-bit, 0-4095) okunur ve arayüzde gösterilir.

Dijital Durum Kontrolü: Kart üzerindeki PF4 butonunun durumu (Basıldı/Beklemede) anlık olarak izlenir ve arayüzde renkli uyarı ile gösterilir.

Sistem Saati: Tiva C, kendi içinde saydığı saati her saniye PC'ye raporlar.

🛠️ Teknik Detaylar ve Kazanımlar
Özel Haberleşme Protokolü: Veri paketleri karışıklığı önlemek için * (Başlangıç) ve # (Bitiş) karakterleri ile kapsüllenmiştir.

Örnek Giden: *S14:53:20# (Saat Ayarı)

Örnek Gelen: *14:53:21,4095,1# (Rapor)

Bellek Optimizasyonu (RAM Management): Tiva C tarafında ağır kütüphaneler (sprintf, stdio.h) yerine, RAM kullanımını minimumda tutan özel string dönüşüm fonksiyonları yazılarak "Stack Overflow" sorunlarının önüne geçilmiştir.

Full-Duplex İletişim: Sistem aynı anda hem veri dinleyip hem de veri gönderebilen (Polling & Timing) bir yapıda kurgulanmıştır.

🧰 Kullanılan Teknolojiler ve Donanımlar
Mikrodenetleyici: Texas Instruments Tiva C Series (TM4C123GH6PM)

IDE (Gömülü): Code Composer Studio (CCS) - C Dili

IDE (Masaüstü): SharpDevelop / Visual Studio - C# (Windows Forms)

Donanım: 16x2 LCD Ekran, Potansiyometre, Butonlar.


Odev1_LCD_Driver: Gömülü LCD Sürücü Kütüphanesi Tasarımı
Bu aşamada hazır kütüphane (lcd.h vb.) kullanmak yerine, LCD'nin datasheet'ini inceleyerek Register Seviyesinde (Register Level) kendi sürücümü yazdım.

Amaç: HD44780 tabanlı 16x2 LCD ekranın çalışma mantığını kavramak ve donanım üzerindeki kontrolü maksimize etmek.

Teknik Detaylar:

GPIO portlarının (PORTB) çıkış olarak yapılandırılması.

Hazır kütüphane kullanmadan, Enable ve RS pinlerinin manuel (bit-banging) kontrolü.

4-bit veri yolu iletişimi ve LCD başlatma (Initialization) sekansının kodlanması.

Kazanım: Hazır kütüphanelere bağımlı kalmadan çevresel birim kontrolü yeteneği.

📂 Odev2_Digital_Clock: Gerçek Zamanlı Dijital Saat Algoritması
Birinci aşamada geliştirdiğim sürücüyü kullanarak, işlemci üzerinde zamanı sayan ve bunu kullanıcıya gösteren bir mantık geliştirdim.

Amaç: Mikrodenetleyici üzerinde zamanlama ve döngü yönetimi becerilerini geliştirmek.

Teknik Detaylar:

Saat, Dakika ve Saniye değişkenleri için taşma mantığının (60 saniye -> 1 dakika) C dili ile algoritmik tasarımı.

SysCtlDelay fonksiyonları ile hassas zamanlama kalibrasyonu.

Ekran yenileme sıklığının optimize edilerek "titreme" (flickering) sorununun çözülmesi.

Kazanım: Algoritma tasarımı ve zaman-kritik döngü yönetimi.

📂 Odev3_LCD_ADC: Analog Sinyal İşleme ve Veri Görselleştirme
Sisteme dış dünyadan veri girişi ekleyerek, Tiva C'nin ADC (Analog-Dijital Dönüştürücü) modülünü aktif ettim ve sensör verilerini işledim.

Amaç: Fiziksel dünyadan alınan analog verilerin dijital ortama aktarılması ve anlamlandırılması.

Teknik Detaylar:

Tiva C ADC0 modülünün ve Sample Sequencer (SS3) biriminin yapılandırılması.

PE3 pininden 12-bitlik (0-4095) analog verinin okunması.

Okunan ham verinin LCD ekran üzerinde, saat bilgisiyle çakışmadan dinamik olarak gösterilmesi.

Kazanım: Gömülü sistemlerde sensör entegrasyonu ve ADC donanım hakimiyeti.


