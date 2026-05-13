# Data Eraser

**Kişisel Veri Gizliliği Otomatı ve Yönetim Platformu**

Data Eraser, internetteki dijital ayak izinizi kontrol altına almanızı sağlayan, veri simsarlarına (data brokers) ve izinsiz rehber sitelerine karşı kişisel verilerinizi savunan otonom bir gizlilik asistanıdır. Dijital gizliliğin bir lüks değil, temel bir insan hakkı olduğu vizyonuyla hareket ederek karmaşık hukuki süreçleri son kullanıcı için tamamen otomatikleştirir.

## Proje Odak Noktaları ve İşleyiş

Sistem, internet üzerindeki kişisel veri sızıntılarını tespit etmek ve yasal yaptırım süreçlerini robotik süreç otomasyonu ile yönetmek üzerine kuruludur:

*   **Otonom Tarama (OSINT ve Web Scraping):** Sistem, kullanıcının adını, e-posta adresini veya diğer temel bilgilerini kullanarak arama motorlarını, veri komisyoncusu (data broker) sitelerini ve herkese açık rehberleri düzenli olarak tarar; kişisel verilerin izinsiz yayınlandığı noktaları tespit eder.
*   **Otomatik "Verimi Sil" Talepleri (Opt-Out Automation):** İhlal tespit edilen sitelere, Avrupa'da GDPR, Kaliforniya'da CCPA veya Türkiye'de KVKK gibi yasal düzenlemelere (Unutulma Hakkı vb.) dayanan resmi "verilerimi sil" talepleri e-posta veya form doldurma botları aracılığıyla otomatik olarak iletilir.
*   **Süreç ve İtiraz Takibi:** Gönderilen taleplerin yasal bekleme süreleri takip edilir. Silme işlemini gerçekleştirmeyen veya süreyi aşan şirketlere otomatik olarak hatırlatıcı e-postalar veya bir üst merciye şikayet tehdidi içeren hukuki ihtar şablonları gönderilir.
*   **Kullanıcı Paneli ve Risk Skoru:** Kullanıcılar, tek bir gösterge panelinden internetteki risk durumlarını, bekleyen/tamamlanan silme taleplerini ve verilerinin temizlenme oranını şeffaf bir şekilde izleyebilir.

## Mimari Yaklaşım ve Teknoloji Yığını

Bu projede bot güvenilirliği, e-posta otomasyonu ve özellikle kullanıcının kendi verilerinin korunması (Zero-Knowledge yaklaşımı) büyük önem taşır:

*   **Tarama ve Otomasyon Motoru:** Python (Selenium, Playwright veya Scrapy). Web sitelerinin "opt-out" formlarını otomatik doldurmak, captcha'ları aşmak (uygun API'lerle) ve veri kazımak için en stabil ve esnek altyapı.
*   **Backend API ve İş Mantığı:** Node.js (NestJS) veya Python (FastAPI). Kullanıcı yönetimini, cron görevlerini (zamanlanmış taramalar) ve e-posta gönderim (SendGrid / Mailgun API) süreçlerini yönetmek için.
*   **Görev Kuyruğu (Task Queue):** Celery (Python) veya BullMQ (Node.js). İnternet taramaları çok uzun sürebileceğinden işlemlerin arka planda asenkron ve güvenli bir şekilde yürütülmesi şarttır.
*   **Veritabanı ve Kritik Güvenlik:** PostgreSQL. Kullanıcının arama yapmak için girdiği verilerin kendisi de son derece hassas olduğu için, bu veriler veritabanında "Encryption at Rest" (örneğin AES-256) standartlarıyla şifrelenir.
*   **Frontend (Yönetim Paneli):** React.js veya Next.js. Kullanıcıya güven hissi veren, minimalist ve durumu net gösteren kurumsal bir dashboard arayüzü.
