# SmartLibrary
mehmet akif ayrılmaz 20230108043 BIP2037
# SmartLibrary - Akıllı Kütüphane Yönetim Sistemi

Bu proje, Üniversite Kütüphanesi için geliştirilmiş, Java tabanlı masaüstü konsol uygulamasıdır. Nesne Yönelimli Programlama (OOP) prensiplerine uygun olarak tasarlanmış olup, veri kalıcılığı için SQLite veritabanı kullanılmıştır.

##  Projenin Amacı
Projenin temel amacı, kütüphanedeki kitap, öğrenci ve ödünç alma süreçlerini dijital ortamda takip etmektir. Katmanlı mimari (Layered Architecture) ve Repository tasarım deseni kullanılarak kodun okunabilirliği, geliştirilebilirliği ve bakımı kolaylaştırılmıştır.

##  Kullanılan Teknolojiler
* **Dil:** Java (JDK 21)
* **Veritabanı:** SQLite
* **Veri Erişimi:** JDBC (Java Database Connectivity)
* **Tasarım Deseni:** Repository Pattern, DAO (Data Access Object) mantığı
* **IDE:** VS Code / IntelliJ IDEA

##  Özellikler
* **Kitap Yönetimi:** Kütüphaneye yeni kitap ekleme ve mevcut kitapları listeleme.
* **Öğrenci Yönetimi:** Öğrenci kaydı oluşturma ve listeleme.
* **Ödünç (Loan) Sistemi:**
    * Bir öğrenciye kitap ödünç verme.
    * Kitabın müsaitlik durumunu kontrol etme (Stok kontrolü).
    * Ödünç alınan kitapları ve tarihleri listeleme.
* **İade Sistemi:** Ödünçteki kitabı geri alma ve iade tarihini güncelleme.
* **Veritabanı Entegrasyonu:** Program kapatılsa bile verilerin kaybolmaması (Persistent Data).

##  Proje Mimarisi ve Sınıflar
Proje, sorumlulukların ayrılması (Separation of Concerns) ilkesine göre şu parçalara ayrılmıştır:

### 1. Varlık Sınıfları (Entities)
Veritabanı tablolarının Java tarafındaki karşılıklarıdır.
* `Book.java`: Kitap bilgilerini (id, başlık, yazar, yıl) tutar.
* `Student.java`: Öğrenci bilgilerini (id, isim, bölüm) tutar.
* `Loan.java`: Ödünç alma işleminin detaylarını (kim, hangi kitabı, ne zaman aldı) tutar.

### 2. Veri Erişim Katmanı (Repository)
Veritabanı ile doğrudan iletişim kuran sınıflardır. SQL sorguları burada çalıştırılır.
* `Database.java`: SQLite bağlantısını kurar ve tablolar yoksa otomatik oluşturur.
* `BookRepository.java`: Kitap ekleme ve listeleme işlemleri.
* `StudentRepository.java`: Öğrenci ekleme ve listeleme işlemleri.
* `LoanRepository.java`: Ödünç verme, iade alma ve kontrol işlemleri. **PreparedStatement** kullanılarak SQL Injection riskine karşı güvenlik sağlanmıştır.

### 3. Ana Uygulama
* `SmartLibraryApp.java`: Kullanıcı ile etkileşime giren, menüleri gösteren ve kullanıcıdan veri alan ana sınıftır.

##  Veritabanı Şeması
Proje ilk çalıştığında `library.db` dosyası otomatik oluşturulur. Tablolar şöyledir:

| Tablo | Açıklama |
|-------|----------|
| **books** | id, title, author, year |
| **students** | id, name, department |
| **loans** | id, bookId, studentId, dateBorrowed, dateReturned |

##  Kurulum ve Çalıştırma

Projeyi kendi bilgisayarınızda çalıştırmak için:

1.  Bu repoyu klonlayın veya indirin.
2.  Proje klasörünü IDE (VS Code veya IntelliJ) ile açın.
3.  **ÖNEMLİ:** `sqlite-jdbc` kütüphanesini (driver) projenin "Referenced Libraries" kısmına eklemeyi unutmayın.
4.  `SmartLibraryApp.java` dosyasını çalıştırın.



