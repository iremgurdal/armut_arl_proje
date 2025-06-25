# armut_arl_proje
# 🧠 ARL ile Hizmet Öneri Sistemi | Armut.com Örneği

Bu proje, Türkiye’nin en büyük online hizmet platformu olan [Armut.com](https://armut.com/) için **Association Rule Learning (ARL)** yöntemini kullanarak hizmet öneri sistemi geliştirmeyi amaçlamaktadır. Kullanıcıların geçmişte aldıkları hizmetler üzerinden yeni hizmetler önerilmesini sağlar.

## 🔍 İş Problemi

Armut, kullanıcılar ile hizmet sağlayıcıları buluşturan bir pazaryeri platformudur. Bu projede, kullanıcıların geçmiş hizmet satın alımlarından yola çıkarak, birlikte alınan hizmet kombinasyonlarını analiz edip **birliktelik kurallarına göre öneriler üretmek** hedeflenmiştir.

## 🧾 Veri Seti

Veri seti, kullanıcıların aldıkları hizmetleri ve bu hizmetlerin kategorilerini içermektedir. Özellikler:

- `UserId`: Müşteri numarası
- `ServiceId`: Her kategoriye ait anonimleştirilmiş servisler
- `CategoryId`: Anonimleştirilmiş kategori numaraları
- `CreateDate`: Hizmetin satın alındığı tarih

## ⚙️ Adımlar

### 1. Veriyi Hazırlama

- **Hizmet Tanımı:** `ServiceId` ve `CategoryId` birleştirilerek tekil hizmet tanımı oluşturuldu.
- **Sepet Tanımı:** Her müşterinin aylık aldığı hizmetler birer sepet olarak tanımlandı.
- **Zaman Dönüşümü:** `CreateDate` sütunu "Yıl-Ay" formatına çevrildi.
- **Sepet ID:** `UserId` ve ay bilgisi birleştirilerek yeni bir `SepetID` oluşturuldu.

### 2. Birliktelik Kuralları Üretme

- Pivot tablo oluşturarak her bir sepetin hangi hizmetleri içerdiği binarize edildi.
- `Apriori` algoritması ile sık hizmet kombinasyonları çıkarıldı.
- `association_rules` fonksiyonu ile **support, confidence, lift** metriklerine göre kurallar üretildi.

### 3. Hizmet Öneri Fonksiyonu

```python
def arl_recommender(rules_df, product_id, rec_count=1):
    ...
