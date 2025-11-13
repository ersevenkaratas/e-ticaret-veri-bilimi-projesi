# 🏆 E-TİCARET VERİLERİ ÜZERİNE UÇTAN UCA VERİ BİLİMİ PROJESİ
## Keşifçi Analiz (EDA) ve K-Means Kümeleme ile Müşteri Segmentasyonu

**Proje Amacı:** Bu proje, Birleşik Krallık merkezli bir e-ticaret şirketinin operasyonel verilerini analiz ederek iş zekası içgörüleri üretmeyi ve Makine Öğrenimi (K-Means) kullanarak müşterileri değerlerine göre segmente etmeyi amaçlamaktadır.

| 🛠️ Kullanılan Teknolojiler | |
| :--- | :--- |
| **Diller** | Python |
| **Kütüphaneler** | Pandas, Numpy, Matplotlib, Seaborn, Scikit-learn (KMeans, StandardScaler) |
| **Ortam** | Jupyter Notebook (Kaggle/Colab) |

***


## 💾 Veri Seti İncelemesi ve Temizlik

**Veri Seti:** İngiltere merkezli bir perakende şirketinin 2010-2011 dönemi arasındaki online satış verilerini içermektedir.

**Veri Temizleme Adımları:**
1. **Veri Tiplerinin Dönüştürülmesi:** Tarih (`InvoiceDate`) sütunu `datetime` formatına dönüştürüldü.
2. **Hatalı Kayıtların Ele Alınması:** İade işlemlerini temsil eden negatif `Quantity` değerleri ve `UnitPrice`'ı sıfır olan kayıtlar çıkarıldı.
3. **Kritik Kayıp Değer İşlemi:** Müşteri segmentasyonu için zorunlu olan `CustomerID` bilgisi eksik olan tüm satırlar analizden çıkarıldı.
4. **Yeni Özellik Türetme:** Toplam satış gelirini hesaplamak için **`Sales`** sütunu (`Quantity` * `UnitPrice`) türetildi.


## 📈 Temel Keşifçi Analiz (EDA) Bulguları

Analiz sonucunda elde edilen en kritik içgörüler şunlardır:

* **Mevsimsellik:** Satışlarda **Ağustos ayından başlayarak Kasım ayında zirveye** ulaşan güçlü bir mevsimsel yoğunluk tespit edilmiştir (Q4 yoğunluğu).
    * **İş Önerisi:** Stok yönetimi ve pazarlama kampanyaları en geç Temmuz ayında başlatılmalıdır.
* **Coğrafi Odak:** Birleşik Krallık dışındaki uluslararası satışların ana kaynağı sırasıyla **Hollanda, İrlanda ve Almanya** pazarlarıdır.
    * **İş Önerisi:** Pazarlama bütçesi ve lojistik odak bu 3 ana pazara yoğunlaştırılmalıdır.
* **Lider Ürün Kategorileri:** En yüksek geliri, **hediyelik eşya/ev dekorasyonu** gibi niş kategorilerdeki ürünler (`Paper Craft, Little Birdie`) getirmektedir.
    * **İş Önerisi:** Yüksek kârlı bu ürünlerin stokları kritik seviyede tutulmalıdır.


## 🤖 Müşteri Segmentasyonu (K-Means Metodolojisi)

Müşteri değerini ölçmek ve Denetimsiz Öğrenme (Unsupervised Learning) ile segmentlere ayırmak için **RFM Analizi** ve **K-Means Kümeleme** kullanılmıştır.

**Adımlar:**
1.  **RFM Metriklerinin Hesaplanması:** Her müşteri için Recency (Yenilik), Frequency (Sıklık) ve Monetary (Harcama) değerleri hesaplandı.
2.  **Veri Ön İşleme:**
    * Verideki yüksek çarpıklığı gidermek için **Logaritmik Dönüşüm** uygulandı.
    * K-Means algoritmasının mesafeyi adil ölçmesi için veriler **Z-Score Standardizasyonu** ile ölçeklendirildi.
3.  **Optimum Küme Sayısının Belirlenmesi:** **Elbow Metodu** kullanılarak en iyi küme sayısının **k=4** olduğu belirlendi.
4.  **K-Means Uygulaması:** Müşteriler 4 segmente ayrılarak, her segmentin ortalama RFM değerleri hesaplandı.


## ✅ Sonuçlar: 4 Müşteri Segmenti ve Stratejiler

RFM analizi sonucunda ortaya çıkan segmentler ve bu segmentlere özel önerilen stratejiler:

| Segment Adı | RFM Özellikleri | Pazarlama Stratejisi |
| :--- | :--- | :--- |
| **Şampiyonlar** | **R: Düşük, F: Yüksek, M: Çok Yüksek** | **Ödüllendirme:** Yeni ürün lansmanlarında öncelik tanıyın ve VIP sadakat programları sunarak elde tutulabilir. |
| **Potansiyel Sadıklar** | **R: Orta, F: Orta, M: Yüksek** | **Teşvik Etme:** Kuponlar veya özel ürün önerileri ile Frekanslarını artırarak Şampiyonlar grubuna geçişleri sağlanabilir. |
| **Yeni Müşteriler** | **R: Düşük, F: Düşük, M: Düşük/Orta** | **Aktivasyon:** İkinci alışverişi teşvik eden hoş geldin indirimleri ile sadakati artırmaya odaklanılabilir. |
| **Risk Altındakiler** | **R: Çok Yüksek, F: Çok Düşük, M: Düşük** | **Geri Kazanım:** Yüksek indirimler içeren "Sizi Özledik" e-postaları veya kampanyaları ile yeniden aktive edilebilir. |
