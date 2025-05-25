# http-and-requests

## `HTTP` METODLARI ve `CRUD` İŞLEMLERİ

| HTTP Metodu | CRUD | Açıklama |
| --- | --- | --- |
| GET | Read | Kaynak okuma |
| POST | Create | Yeni kaynak oluşturma |
| PUT | Update | Kaynağı tamamen güncelleme |
| PATCH | Update | Kaynağın bir kısmını güncelleme |
| DELETE | Delete | Kaynak silme |

## JSON ve XML Formatları

JSON

```json
{
  "userId": 1,
  "id": 1,
  "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
  "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
}
```

XML

```xml
<post>
  <userId>1</userId>
  <id>1</id>
  <title>sunt aut facere repellat provident occaecati excepturi optio reprehenderit</title>
  <body>quia et suscipit suscipit recusandae consequuntur expedita et cum reprehenderit molestiae ut ut quas totam nostrum rerum est autem sunt rem eveniet architecto</body>
</post>
```

## RESTful API ve HTTP İstekleri

### 1- RESTful API Nedir?

- Bir lokantadasın ve garson sana menüyü getiriyor. Sen ne istediğini söylüyorsun, o da mutfağa iletiyor ve yemeğini getiriyor. RESTful API da tam olarak böyle çalışır:
    - Sen = Bilgisyar programın (istemci)
    - Garson = API
    - Mutfak = Sunucu (Server)
    - Menü = API dokümantasyonu
- Örneğin, hava durumu uygulaman açılıyor ve “Bugün İstanbul’da hava nasıl?” diye soruyor. Uygulama bir API’ ye (hava durumu servisine) bu soruyu soruyor, API de sunucudan bilgiyi alıp sana gösteriyor

### 2- HTTP: İnternetin Dili

- HTTP, bilgisayarların birbiriyle konuşma şeklidir. Bir mektup yazdığını düşün:
    - Zarfın üzerindeki adres = URL
    - Mektubun türü = HTTP Metodu (GET, POST, PUT, DELETE)
    - Mektubun İçeriği = Body (İçerik)

Temel HTTP Metodları

1. GET = “Bana bilgi ver” (Soru sormak gibi)
    1. Örnek: “Bana kullanıcı listesini ver”
2. POST = “Yeni bir şey oluştur” (Sipariş vermek gibi)
    1. Örnek: “Yeni bir kullanıcı kaydı oluştur”
3. PUT = “Varolan bir şeyi tamamen güncelle” (Bilgileri değiştirmek gibi)
    1. Örnek: “Kullanıcının tüm bilgilerini güncelle”
4. DELETE = “Bir şeyi sil” (Çöp kutusuna atmak gibi)
    1. Örnek: “Bu kullanıcıyı sil”

### 3- JSON ve XML: Verinin Paketlenme Şekli

- API ‘lar bilgiyi genellikle iki şekilde gönderirler

JSON(Javascript Object Notation)

```json
{
  "ad": "Ahmet",
  "yas": 25,
  "sehir": "İstanbul",
  "hobiler": ["futbol", "müzik", "yüzme"]
}
```

- Günümüzde en popüler format
- Javascriptteki nesnelere benzer
- Hafif ve okuması kolay

**XML (eXtensible Markup Language)**

```xml
<kisi>
  <ad>Ahmet</ad>
  <yas>25</yas>
  <sehir>İstanbul</sehir>
  <hobiler>
    <hobi>futbol</hobi>
    <hobi>müzik</hobi>
    <hobi>yüzme</hobi>
  </hobiler>
</kisi>
```

- HTML’e benzer bir yapı
- Daha eski sistemlerde kullanılır
- Daha fazla karakter kullanılır (daha ağır)

### 4- PYTHON’DA REQUESTS KÜTÜPHANESİYLE ÇALIŞMA

KURULUM

- Öncelikle bu kütüphaneyi import etmemiz ve download etmemiz gerekiyor
    - İmpor işlemi = `import requests`
    - Download işlemi = `pip install requests`

GET Örneği (Bilgi Almak)

```python
import requests

# Bir web sayfasının içeriğini alalım
cevap = requests.get('https://jsonplaceholder.typicode.com/todos/1')

print("Durum Kodu:", cevap.status_code)  # 200 başarılı demek
print("İçerik Türü:", cevap.headers['content-type'])
print("JSON Verisi:", cevap.json())
```

POST Örneği (Bilgi Göndermek)

```python
import requests

yeni_gorev = {
    "userId": 1,
    "title": "Alışveriş yap",
    "completed": False
}

cevap = requests.post('https://jsonplaceholder.typicode.com/todos', json=yeni_gorev)

print("Durum Kodu:", cevap.status_code)  # 201 oluşturuldu demek
print("Oluşturulan Görev:", cevap.json())
```

PUT Örneği (Güncelleme)

```python
import requests

guncellenen_gorev = {
    "userId": 1,
    "title": "Alışveriş yap (acil!)",
    "completed": False
}

cevap = requests.put('https://jsonplaceholder.typicode.com/todos/1', json=guncellenen_gorev)

print("Durum Kodu:", cevap.status_code)
print("Güncellenen Görev:", cevap.json())
```

DELETE Örneği (Silme)

```python
import requests

cevap = requests.delete('https://jsonplaceholder.typicode.com/todos/1')

print("Durum Kodu:", cevap.status_code)  # 200 başarılı demek
print("Silme İşlemi Sonrası:", cevap.json())  # Genellikle boş döner
```

## 7. Adım Adım Öğrenme Planı

1. **Hafta 1**: GET istekleriyle çeşitli API'lerden veri çekmeyi öğren
    - JSONPlaceholder
    - Public APIs listesinden örnekler
2. **Hafta 2**: POST ve form verisi göndermeyi öğren
    - Kullanıcı kaydı simülasyonu
    - Yorum gönderme örneği
3. **Hafta 3**: Hata yönetimi ve header'ları anla
    - Yetkilendirme (Authorization)
    - Content-Type ayarları
4. **Hafta 4**: Gerçek bir proje yap
    - Hava durumu uygulaması
    - Haber çekme uygulaması

## 8. Pratik İpuçları

1. **API Dokümantasyonunu Oku**: Her API'nin kendine özel kuralları vardır
2. **Postman Kullan**: Önce Postman'de test et, sonra koda dök
3. **Küçük Adımlarla İlerle**: Önce basit GET istekleri, sonra kompleks senaryolar
4. **Hata Mesajlarını Oku**: Hatalar aslında sana yol gösterir

## 9. Sıkça Sorulan Sorular

**S: API key nedir?**

C: Bir nevi şifre. API'yi kullanma iznin. Herkesin kendi key'i olur.

**S: Neden 404 hatası alıyorum?**

C: Yanlış URL yazmış olabilirsin. Adresi kontrol et.

**S: JSON verisinde nasıl gezinirim?**

C: Python'da sözlük gibi kullanabilirsin: `veri['anahtar']`

**S: API yavaş çalışıyor ne yapmalıyım?**

C: `timeout` parametresi ekle: `requests.get(url, timeout=3)`
