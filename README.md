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

# UML Sınıf Diyagramı:

> ![image](https://user-images.githubusercontent.com/24902892/209235266-977d6631-ba71-46e6-9ba3-2d705bca03b1.png)

>>"app: Bu sınıf ana Express uygulama nesnesini temsil eder. HTTP GET isteklerini işlemek için rotaları tanımlamak için kullanılan tek bir get() yöntemine sahiptir."

>>"articles: Bu sınıf, haber makalelerini temsil eden nesneleri saklayan bir dizidir. Her makale nesnesinin üç özniteliği vardır: başlık, url ve kaynak."

>>"newspapers: Bu sınıf, farklı haber web sitelerini temsil eden nesneleri depolayan bir dizidir. Her web sitesi nesnesinin üç özniteliği vardır: ad, adres ve taban."

>>"PORT: Bu sınıf, Express sunucusunun dinleyeceği bağlantı noktası numarasını temsil eden bir sabittir. process.env.PORT ortam değişkeni kullanılarak veya ortam değişkeni ayarlanmamışsa varsayılan 8000 değeri kullanılarak başlatılır."

# ER Diyagramı:

>![image](https://user-images.githubusercontent.com/24902892/209235975-060e766d-4881-4f80-9aff-86fc2cdc54eb.png)

>>"articles: Bu varlık haber makalelerini temsil eder. Üç özniteliği vardır: başlık, url ve kaynak."

>>"newspapers: Gazeteler: Bu varlık farklı haber web sitelerini temsil eder. Üç özniteliği vardır: isim, adres ve taban."

>>"Her makale belirli bir haber web sitesiyle ilişkilendirildiğinden, articles ve newspapers varlıkları arasında da bir ilişki vardır."


# API Test Örneği 1: Makaleleri Al

## Test Durumu Açıklaması:

Bu test senaryosu, API'nin beklendiği gibi farklı haber web sitelerinden haber makalelerini alabildiğini doğrulamayı amaçlamaktadır.

## Test Adımları:

1. API'nin `/` uç noktasına bir GET isteği gönderin.
2. API'nin bir `200 OK` HTTP durum kodu döndürdüğünü doğrulayın.
3. API'nin yanıt gövdesinde haber makalelerinden oluşan bir JSON dizisi döndürdüğünü doğrulayın.
4. Dizideki her makalenin bir `title`, `url` ve `source` özniteliğine sahip olduğunu doğrulayın.

## Beklenen Sonuçlar:

- API bir `200 OK` HTTP durum kodu döndürür.
- API, yanıt gövdesinde haber makalelerinden oluşan bir JSON dizisi döndürür.
- Dizideki her makalenin bir `title`, `url` ve `source` özniteliği vardır.

## Python Örnek Test Case Kodu:

```
$ npm install -D jest axios
$ touch __tests__/api.test.js
const axios = require('axios');

describe('API Test Scenario: Get Articles', () => {
  it('should verify that the API returns 200 OK and a list of articles in the response body', async () => {
    const response = await axios.get('http://localhost:8000/');

    expect(response.status).toBe(200);
    expect(Array.isArray(response.data)).toBe(true);
    expect(response.data[0]).toHaveProperty('title');
    expect(response.data[0]).toHaveProperty('url');
    expect(response.data[0]).toHaveProperty('source');
  });
});
```

## Örnek Test Sorgu Yanıtı:

```sh
$ npm test
> jest
API Test Scenario: Get Articles
  √ should verify that the API returns 200 OK and a list of articles in the response body (5ms)
Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        1.222s
Ran all test suites.
```


| Proje: REST API Test Ortamı |
|-----------------------------|

| Hazırlayan      | Danışman         |
| --------------- | ---------------- |
| Mehmet KESİMALİOĞLU | Dr. Gökhan ALTAN |





