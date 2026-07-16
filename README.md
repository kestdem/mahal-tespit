# Zemin Dönüşüm Ön Tespit Formu

Mobil uyumlu zemin ön tespit uygulaması. Kullanıcı girişi (Firebase Authentication) ve bulut veri saklama (Firebase Realtime Database) ile çalışır. Her kullanıcı yalnızca kendi verilerini görür; veriler cihazdan bağımsız olarak buluta kaydedilir.

## Özellikler

- E-posta / şifre ile giriş ve kayıt (Firebase Authentication)
- Veriler kullanıcı hesabına özel olarak Realtime Database'de saklanır
- Mahal başına m² alanı girişi ve raporda toplam m²
- Mevcut zemin türü, deformasyon derecesi, tesviye, süpürgelik, duvar hattı, kapı kesimi, notlar
- WhatsApp/e-posta için rapor kopyalama ve Excel (CSV) dışa aktarma

## Kurulum

### 1. Firebase projesi oluştur
[Firebase Console](https://console.firebase.google.com) → yeni proje.

### 2. Web uygulaması ekle
Proje Ayarları → "Web uygulaması" ekle → verilen `firebaseConfig` bilgilerini kopyala.

### 3. `index.html` içindeki config'i doldur
Dosyada `BURAYA_...` yazan alanları kendi değerlerinle değiştir:

```js
const firebaseConfig = {
    apiKey: "...",
    authDomain: "...",
    databaseURL: "...",
    projectId: "...",
    storageBucket: "...",
    messagingSenderId: "...",
    appId: "..."
};
```

### 4. Authentication'ı aç
Authentication → Sign-in method → **E-posta/Şifre** yöntemini etkinleştir.

### 5. Realtime Database oluştur
Realtime Database → veritabanı oluştur. Aşağıdaki kuralları kullan (her kullanıcı sadece kendi verisine erişir):

```json
{
  "rules": {
    "users": {
      "$uid": {
        ".read": "$uid === auth.uid",
        ".write": "$uid === auth.uid"
      }
    }
  }
}
```

### 6. Yayınla
Dosya statik olduğu için doğrudan **GitHub Pages** ile yayınlanabilir:
Repo → Settings → Pages → Branch: `main` / root → Save.

> Not: Firebase web API anahtarı gizli değildir, istemci tarafında görünmesi normaldir. Güvenlik yukarıdaki Database kuralları ile sağlanır.

## Dosyalar
- `index.html` — tek dosyalık uygulama (HTML + Tailwind + Firebase)
- `README.md` — bu dosya
