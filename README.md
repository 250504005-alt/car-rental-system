# Car Rental System

Software Design and Architecture dersi kapsamında geliştirilen **Car Rental System** projesi.

## Proje Özeti
Müşterilerin tarih aralığına ve araç tipine göre müsait araçları arayıp rezervasyon yapabildiği; ödeme, teslim ve iade süreçlerinin yönetildiği katmanlı mimariye sahip Java uygulamasıdır. Yönetici tarafı araç filosunu, fiyatları ve rezervasyonları yönetir.

## Teknolojiler
- **Dil:** Java 17+
- **Derleme ve Bağımlılık:** Maven
- **IDE:** NetBeans
- **Test:** JUnit 5
- **Veritabanı:** H2 (gömülü) + JDBC

## Klasör Yapısı
- `docs/adr/`: Mimari Karar Kayıtları (ADR)
- `docs/diagrams/`: Diyagram kaynakları ve görselleri
- `docs/report/`: Final raporu
- `src/main/java/com/carrental/`: Katmanlı uygulama kaynak kodları
- `src/test/java/com/carrental/`: JUnit 5 testleri
