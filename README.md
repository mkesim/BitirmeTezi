# API Testi

API testi, bir API programının performansını ve yeteneklerini farklı ortamlarda ve yöntemlerle analiz etmeyi amaçlayan bir yazılım testidir. 

## Çalışma Özeti

Bu projede HTTP proxy entegrasyonu kullanılarak inşa edilecek olan Gateway Api mekanizması kullanılarak Rest Api türünde bir test ortamı hazırlanacaktır. Test süreci ve sonuçların analizi, API programının web teknolojilerini kullanarak hızlı ve verimli bir şekilde istek ve yanıt veri alışverişi yapabilmesini sağlamak için yapılacaktır. Bu projenin amacı API'nin düzgün çalışmasını sağlamaktır.

| Önemli Adımlar      | Açıklama                                              |
|--------------------|-------------------------------------------------------|
| Test Ortamı Hazırlama | Gateway Api mekanizması kullanılarak test ortamı oluşturulacak |
| Test Süreci       | Test süreci ve sonuçların analizi yapılacak          |
| Amaç               | API'nin düzgün çalışmasını sağlamak                   |


# Use Case Diyagramı:

                                            +----------------+
                                            |                |
                                            |  News Scraper  |
                                            |                |
                                            +--------+-------+
                                                     |
                                                     |
                           +--------------------------|---------------------------+
                           |                         |                         |
                           |                         |                         |
                           |                         |                         |
        +------------------+                  +-------v-------+            +-------v-------+
        |                  |                  |               |            |               |
        |  Express Server  +----------------->+   Newspaper   |            |   Newspaper   |
        |                  |                  |               |            |               |
        +--------+---------+                  +-------+-------+            +-------+-------+
                 |                                   |                         |
                 |                                   |                         |
                 |                                   |                         |
        +--------v---------+                  +-------v-------+            +-------v-------+
        |                  |                  |               |            |               |
        |  Axios & Cheerio +----------------->+   Article    |            |   Article    |
        |                  |                  |               |            |               |
        +------------------+                  +---------------+            +---------------+

> Bu diyagramda API, Gazete web sitelerine HTTP istekleri göndermek ve Makale bağlantılarını çıkarmak için ortaya çıkan HTML'yi ayrıştırmak için Axios ve Cheerio kütüphanelerini kullanan Express Sunucusu ile etkileşim halindedir. Ekspres Sunucu, 8000 numaralı bağlantı noktasındaki HTTP isteklerini dinler ve tüm gazetelerden topladığı makalelerin listesiyle veya uygun uç nokta talep edilirse belirli bir gazeteden makalelerin listesiyle yanıt verir.

