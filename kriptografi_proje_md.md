
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

## Temel Bileşenlerin Geliştirilmesi

### Caesar Şifreleme
```python
def caesar_encrypt(text, shift):
    result = ""
    for char in text:
        if char.isalpha():
            offset = 65 if char.isupper() else 97
            result += chr((ord(char) - offset + shift) % 26 + offset)
        else:
            result += char
    return result

def caesar_decrypt(text, shift):
    return caesar_encrypt(text, -shift)
```
### Caesar Şifreleme örnek

def caesar_encrypt(text, shift):
    result = ""
    for char in text:
        if char.isalpha():
            offset = 65 if char.isupper() else 97
            result += chr((ord(char) - offset + shift) % 26 + offset)
        else:
            result += char
    return result

def caesar_decrypt(text, shift):
    return caesar_encrypt(text, -shift)

# Örnek kullanım
text = "Merhaba Dünya!"
sifreli = caesar_encrypt(text, 3)
cozulmus = caesar_decrypt(sifreli, 3)

print("Şifreli:", sifreli)
print("Çözülmüş:", cozulmus)
```

### Vigenère Şifreleme
```python
def vigenere_encrypt(plaintext, key):
    key = key.upper()
    ciphertext = ""
    for i, char in enumerate(plaintext):
        if char.isalpha():
            offset = 65 if char.isupper() else 97
            key_char = ord(key[i % len(key)]) - 65
            ciphertext += chr((ord(char) - offset + key_char) % 26 + offset)
        else:
            ciphertext += char
    return ciphertext
```
###
def vigenere_encrypt(plaintext, key):
    key = key.upper()
    ciphertext = ""
    for i, char in enumerate(plaintext):
        if char.isalpha():
            offset = 65 if char.isupper() else 97
            key_char = ord(key[i % len(key)]) - 65
            ciphertext += chr((ord(char) - offset + key_char) % 26 + offset)
        else:
            ciphertext += char
    return ciphertext

# Örnek kullanım
mesaj = "Merhaba Dünya"
anahtar = "ANAHTAR"
sifreli = vigenere_encrypt(mesaj, anahtar)

print("Şifreli mesaj:", sifreli)
```



### AES ile Simetrik Şifreleme
```python
from cryptography.fernet import Fernet

# Anahtar üret
key = Fernet.generate_key()
cipher = Fernet(key)

# Şifreleme
token = cipher.encrypt(b"gizli mesaj")
# Deşifre
original = cipher.decrypt(token)
```

from cryptography.fernet import Fernet

key = Fernet.generate_key()
cipher = Fernet(key)

# Şifreleme
token = cipher.encrypt(b"gizli mesaj")
# Deşifre
original = cipher.decrypt(token)

print("Anahtar:", key.decode())
print("Şifreli:", token.decode())
print("Çözülmüş:", original.decode())

```



### SHA256 ve HMAC ile İmza
```python
import hmac
import hashlib

message = b"Mesaj metni"
key = b"gizli_anahtar"
signature = hmac.new(key, message, hashlib.sha256).hexdigest()
```
###
import hmac
import hashlib

message = b"Mesaj metni"
key = b"gizli_anahtar"
signature = hmac.new(key, message, hashlib.sha256).hexdigest()

print("HMAC İmza:", signature)
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
