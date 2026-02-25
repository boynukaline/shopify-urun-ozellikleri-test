# Shopify Ürün Özellikleri Alanı (Product Features Section)

## Proje Hakkında
Bu proje, Shopify ürün sayfaları için ürün metafield'larından (metaalanlar) veri çeken, dinamik ve özelleştirilebilir bir "Ürün Özellikleri" alanı oluşturur. Kod yapısı sade, okunabilir ve Shopify Online Store 2.0 standartlarına uygun şekilde geliştirilmiştir.

## Teknik Özellikler ve Gereksinimler
Proje, ödevde belirtilen aşağıdaki teknik kriterleri tam olarak karşılamaktadır:

- **Metafield Kullanımı:** Veriler `custom.features` (Multi-line text) alanından çekilmektedir.
- **Dinamik İçerik:** Her yeni satır otomatik olarak bir liste maddesine (`<li>`) dönüştürülür.
- **Hata Yönetimi:** 
  - `strip` ve `strip_newlines` filtreleri kullanılarak satır başındaki/sonundaki gereksiz boşluklar temizlenir.
  - Boş satırların render edilmesi engellenmiştir.
- **Koşullu Render:** Metafield verisi boşsa, section sayfada tamamen gizlenir (hiçbir HTML çıktısı üretilmez).
- **Esnek Tasarım:** Schema üzerinden başlık, arka plan rengi ve iç boşluk (padding) ayarlanabilir.

## Kurulum ve Kullanım

### 1. Metafield Tanımlama
Kodun çalışması için Shopify Admin panelinde şu tanımlamanın yapılması gerekir:
- **Namespace:** `custom`
- **Key:** `features`
- **Type:** `Multi-line text`

### 2. Dosya Yapısı
- `sections/product-features.liquid` dosyasını temanızın `/sections` klasörüne ekleyin.
- Bu section sadece `product` şablonlarında çalışacak şekilde (`enabled_on`) sınırlandırılmıştır.

### 3. Kullanım
Section'ı `product.json` dosyanıza manuel olarak ekleyebilir veya Shopify Tema Özelleştirici (Customize) üzerinden "Bölüm Ekle" diyerek sayfaya dahil edebilirsiniz.

## Kod Mantığı (Logic)
1. **Veri Kontrolü:** İlk aşamada metafield'ın boş olup olmadığı kontrol edilir.
2. **Satır Ayrıştırma:** Çok satırlı metin, `newline_to_br` ve `split` filtreleri kullanılarak bir diziye (array) dönüştürülür.
3. **Temizlik:** `for` döngüsü içinde her bir satır `strip` işleminden geçirilerek sadece dolu olan satırlar liste elemanı olarak basılır.
4. **Schema:** `enabled_on` yapısı kullanılarak section'ın sadece ürün sayfalarında görünmesi sağlanmış, kullanıcı dostu ayarlar eklenmiştir.
