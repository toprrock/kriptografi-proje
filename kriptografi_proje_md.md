
## Giriş
Bu yol haritası, Python programlama dili kullanılarak temel kriptografi algoritmalarının nasıl geliştirileceği ve test edileceğine dair adım adım bir rehber sunar. Bu projede, klasik şifreleme yöntemleri (Caesar, Vigenère), modern simetrik şifreleme (AES) ve temel imzalama algoritmaları (SHA256 + HMAC) uygulanacaktır. Bu bilgiler eğitim ve araştırma amaçlıdır.

## Ön Koşullar
- **Kütüphaneler**:
  - `cryptography`: Modern şifreleme algoritmaları için (`pip install cryptography`)
  - `hashlib` ve `hmac`: Python’un yerleşik modülleri
- **Bilgi Gereksinimleri**:
  - Python temelleri
  - Temel kriptografi bilgisi
- **Araçlar**:
  - Visual Studio Code veya benzeri bir IDE

## Test Ortamını Kurma
1. Python yüklü olduğundan emin olun.
2. Gerekli kütüphaneleri yükleyin:
   ```bash
   pip install cryptography
   ```
3. Test dosyalarını ve örnek veri girdilerini oluşturun (metin dosyaları vb.).


### Caesar Şifreleme
```python
def caesar_encrypt(text, shift):
    result = ""
    for char in text:
        if char.isalpha():
            shifted = ord(char) + shift
            if char.islower():
                if shifted > ord('z'):
                    shifted -= 26
            elif char.isupper():
                if shifted > ord('Z'):
                    shifted -= 26
            result += chr(shifted)
        else:
            result += char
    return result

def caesar_decrypt(text, shift):
    return caesar_encrypt(text, -shift)

# Örnek
sifreli = caesar_encrypt("Merhaba", 3)
print("Şifreli:", sifreli)
print("Çözülmüş:", caesar_decrypt(sifreli, 3))

```


### Vigenère Şifreleme
```
def vigenere_encrypt(text, key):
    result = ""
    key = key.lower()
    for i, char in enumerate(text):
        if char.isalpha():
            shift = ord(key[i % len(key)]) - ord('a')
            result += caesar_encrypt(char, shift)
        else:
            result += char
    return result

# Caesar fonksiyonu yukarıdan kullanılmalı

# Örnek
print("Vigenère Şifreli:", vigenere_encrypt("Merhaba", "anahtar"))
```


### AES ile Simetrik Şifreleme
```from cryptography.fernet import Fernet

# Anahtar oluştur ve kullan
key = Fernet.generate_key()
f = Fernet(key)

# Mesaj şifrele
sifreli = f.encrypt(b"gizli mesaj")
cozulmus = f.decrypt(sifreli)

print("Şifreli:", sifreli.decode())
print("Çözülmüş:", cozulmus.decode())

```





### SHA256 ve HMAC ile İmza
```python
import hashlib
import hmac

mesaj = b"deneme"
anahtar = b"anahtar"

imza = hmac.new(anahtar, mesaj, hashlib.sha256).hexdigest()

print("HMAC SHA256:", imza)

```




## Gelişmiş Geliştirmeler

### Komut Satırından Kullanım
Python `argparse` ile betiklerin terminalden çalıştırılabilir hale getirilmesi:
```python
import argparse
# argparse kullanılarak seçilen şifreleme algoritması ve metin işlenebilir.
```

### GUI (İsteğe Bağlı)
Tkinter ile basit bir kullanıcı arayüzü eklenebilir.

## Geliştirmelerin Test Edilmesi
- Caesar ve Vigenère şifreleme için örnek girdiler kullanılarak şifrelenmiş metinlerin geri çözümlenmesi sağlanmalı.
- AES şifreleme test edilerek, aynı mesajdan farklı token’lar üretildiği gösterilmeli.
- SHA256 + HMAC için farklı anahtarlar ile aynı mesajın imzalanması denemeli.

## Karşı Önlemler ve En İyi Uygulamalar
- Sabit anahtarlar yerine dinamik anahtarlar kullanın.
- AES için `cryptography` kütüphanesinin sağladığı güvenli modları tercih edin.
- Anahtar yönetimi için çevresel değişkenleri kullanın.

## Sonuç
Bu yol haritası, Python ile temel kriptografi algoritmalarının nasıl uygulanabileceğini göstermektedir. Bu bilgiler, güvenli veri iletimi ve bütünlük doğrulaması gibi alanlarda temel oluşturur. Proje, hem eğitici hem de pratik örneklerle desteklenmiştir.




## **IMPORT RSA** 
```

print(" Anahtar çifti oluşturuluyor...")
public_key, private_key = rsa.newkeys(512)

with open("public_key.pem", "wb") as pub_file:
    pub_file.write(public_key.save_pkcs1())

with open("private_key.pem", "wb") as priv_file:
    priv_file.write(private_key.save_pkcs1())

print(" Anahtarlar 'public_key.pem' ve 'private_key.pem' olarak kaydedildi.\n")

mesaj = input(" Şifrelemek istediğiniz mesajı yazın: ")
mesaj_bytes = mesaj.encode()

print("\n Mesaj şifreleniyor...")
sifreli = rsa.encrypt(mesaj_bytes, public_key)

print(" Şifreli mesaj (baytlar halinde):", sifreli)

with open("sifreli_mesaj.bin", "wb") as f:
    f.write(sifreli)
print(" Şifreli mesaj 'sifreli_mesaj.bin' dosyasına yazıldı.\n")

with open("sifreli_mesaj.bin", "rb") as f:
    sifreli_dosyadan = f.read()

print(" Mesaj çözümleniyor...")
cozulmus = rsa.decrypt(sifreli_dosyadan, private_key)

print(" Çözülmüş mesaj:", cozulmus.decode())
```

## RSA Kullanımı İçin Gerekli Malzemeler (Ön Koşullar)
 Kütüphaneler
RSA algoritmasını basit bir şekilde uygulayabilmek için aşağıdaki kütüphaneyi yüklemen yeterli:

bash
Kopyala
Düzenle
pip install rsa
Bu kütüphane sayesinde fazla detaya girmeden kolayca şifreleme ve şifre çözme işlemleri yapabilirsin.

 Bilmen Gerekenler
RSA’yı kullanabilmek için Python hakkında çok ileri düzey bilgilere gerek yok. Şunları bilmen yeterli:

Değişken, fonksiyon gibi temel Python kavramları

Birkaç satır kodu yazabilmek

Basit düzeyde "şifreleme" nedir, ne işe yarar bilmek

 Hangi Araçlar Lazım?
Kodları yazmak ve çalıştırmak için şunlar yeterli olur:
Visual Studio Code, PyCharm veya Thonny gibi bir editör (ya da basit bir metin düzenleyici)

Terminal (Komut Satırı) ya da editörün kendi “Run” tuşu

 RSA İçin Test Ortamı Nasıl Kurulur?
-**Adım 1: Python yüklü mü kontrol et-**
Terminale şunu yaz:

bash
Kopyala
Düzenle
python --version
Eğer bir versiyon çıkıyorsa her şey yolunda.

   -**Adım 2: Gerekli kütüphaneyi kur-**
bash
Kopyala
Düzenle
pip install rsa
  -**Adım 3: Kodları .py dosyası olarak yaz-**
##RSA işlemlerini yapacağın kodları bir .py dosyasına yaz (örneğin: rsa_ornek.py).

   -**Adım 4: Test etmek için bir mesaj seç-**
##Örneğin: "Selam Dünya!" gibi bir metni şifreleyip çözerek test et.
