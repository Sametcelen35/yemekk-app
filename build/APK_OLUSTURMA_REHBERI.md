# 📱 Seninle Mutfakta - APK Oluşturma Rehberi

Bu rehber, kendi bilgisayarınızda **Android APK** dosyası oluşturmanız için adım adım talimatları içerir.

---

## 🔧 Gereksinimler

Bilgisayarınızda aşağıdakilerin kurulu olması gerekiyor:

1. **Node.js** (v16 veya üstü) - [İndir](https://nodejs.org/)
2. **Android Studio** - [İndir](https://developer.android.com/studio)
3. **Java JDK** (Android Studio ile birlikte gelir)

---

## 📥 Adım 1: Projeyi İndirin

1. Aşağıdaki linke tıklayın ve projeyi indirin:
   
   **İndirme Linki:** `https://cooking-duo.preview.emergentagent.com/seninle-mutfakta-mobile.zip`

2. ZIP dosyasını bir klasöre çıkartın (örn: `C:\Projects\seninle-mutfakta-mobile`)

---

## ⚙️ Adım 2: Android Studio Kurulumu

### Windows:

1. **Android Studio'yu indirin ve kurun**
2. Android Studio'yu açın
3. "More Actions" > "SDK Manager" tıklayın
4. "SDK Platforms" sekmesinde **Android 13 (Tiramisu)** seçin
5. "SDK Tools" sekmesinde şunları seçin:
   - Android SDK Build-Tools
   - Android SDK Command-line Tools
   - Android Emulator
   - Android SDK Platform-Tools
6. "Apply" tıklayın ve kurulumu tamamlayın

### macOS:

1. **Android Studio'yu indirin ve kurun**
2. Homebrew ile Java kurun:
   ```bash
   brew install openjdk@17
   ```
3. Android Studio'yu açın ve SDK Manager'dan gerekli paketleri kurun

---

## 🔐 Adım 3: Ortam Değişkenlerini Ayarlayın

### Windows:

1. **Başlat** menüsünde "Ortam Değişkenleri" arayın
2. "Sistem değişkenlerini düzenle" tıklayın
3. "Ortam Değişkenleri" butonuna tıklayın
4. "Sistem değişkenleri" altında "Yeni" tıklayın

Şu değişkenleri ekleyin:

```
ANDROID_HOME = C:\Users\KULLANICI_ADINIZ\AppData\Local\Android\Sdk
JAVA_HOME = C:\Program Files\Android\Android Studio\jbr
```

5. "Path" değişkenini düzenleyin ve şunları ekleyin:
```
%ANDROID_HOME%\platform-tools
%ANDROID_HOME%\tools
%JAVA_HOME%\bin
```

### macOS/Linux:

`~/.bashrc` veya `~/.zshrc` dosyanıza ekleyin:

```bash
export ANDROID_HOME=$HOME/Library/Android/sdk
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/platform-tools
export JAVA_HOME=/Applications/Android\ Studio.app/Contents/jbr/Contents/Home
```

Sonra terminali yeniden başlatın:
```bash
source ~/.zshrc  # veya source ~/.bashrc
```

---

## 📦 Adım 4: Projeyi Hazırlayın

1. **Terminali açın** (Windows: CMD veya PowerShell, macOS: Terminal)

2. Proje klasörüne gidin:
   ```bash
   cd C:\Projects\seninle-mutfakta-mobile
   # veya macOS/Linux için
   cd ~/Projects/seninle-mutfakta-mobile
   ```

3. **Node modüllerini yükleyin:**
   ```bash
   npm install
   ```

4. **Expo CLI'yi global olarak yükleyin:**
   ```bash
   npm install -g expo-cli
   ```

---

## 🚀 Yöntem 1: EAS Build (Önerilen - En Kolay)

### a) EAS CLI'yi kurun:
```bash
npm install -g eas-cli
```

### b) Expo hesabı oluşturun:
```bash
eas login
```
(Henüz hesabınız yoksa: https://expo.dev/signup)

### c) Projeyi EAS'a bağlayın:
```bash
eas build:configure
```

### d) APK oluşturun:
```bash
eas build -p android --profile preview
```

### e) Build tamamlandığında:
- Terminal'de bir **download linki** göreceksiniz
- Linke tıklayıp APK'yı indirin
- APK'yı telefonunuza gönderin (Google Drive, email, vs.)
- Telefonunuzda APK'yı açıp yükleyin

**Süre:** 15-20 dakika

---

## 🛠️ Yöntem 2: Local Build (Daha Teknik)

### a) Android klasörünü oluşturun:
```bash
npx expo prebuild
```

### b) Gradle ile APK oluşturun:

**Windows:**
```bash
cd android
gradlew assembleRelease
```

**macOS/Linux:**
```bash
cd android
./gradlew assembleRelease
```

### c) APK'yı bulun:
APK şu konumda oluşacak:
```
android/app/build/outputs/apk/release/app-release.apk
```

**Süre:** 10-15 dakika

---

## 📱 Adım 5: APK'yı Telefonunuza Yükleyin

### Android Telefonda:

1. **APK dosyasını telefonunuza gönderin:**
   - Google Drive
   - Email
   - USB kablo ile

2. **Bilinmeyen Kaynaklara İzin Verin:**
   - Ayarlar > Güvenlik
   - "Bilinmeyen kaynaklardan yüklemeye izin ver" seçeneğini açın

3. **APK'yı yükleyin:**
   - Dosya yöneticisinden APK'yı açın
   - "Yükle" butonuna basın
   - Kurulum tamamlandığında "Aç" deyin

---

## 🐛 Sorun Giderme

### Hata: "SDK location not found"

**Çözüm:** `android/local.properties` dosyası oluşturun:

**Windows:**
```
sdk.dir=C:\\Users\\KULLANICI_ADINIZ\\AppData\\Local\\Android\\Sdk
```

**macOS/Linux:**
```
sdk.dir=/Users/KULLANICI_ADINIZ/Library/Android/sdk
```

---

### Hata: "JAVA_HOME is not set"

**Çözüm:** Java yolunu kontrol edin:

```bash
# Java kurulu mu kontrol et
java -version

# JAVA_HOME'u ayarla
# Windows (PowerShell):
$env:JAVA_HOME="C:\Program Files\Android\Android Studio\jbr"

# macOS/Linux:
export JAVA_HOME=/Applications/Android\ Studio.app/Contents/jbr/Contents/Home
```

---

### Hata: "Gradle build failed"

**Çözüm:**
```bash
cd android
# Windows:
gradlew clean
# macOS/Linux:
./gradlew clean

cd ..
npx expo prebuild --clean
```

---

### Hata: "Unable to load script"

**Çözüm:** Metro bundler'ı yeniden başlatın:
```bash
npm start -- --reset-cache
```

---

## 🎯 Test Etme

APK yüklendikten sonra:

1. **Uygulamayı açın**
2. **Kayıt Ol** butonuna basın
3. Email ve şifre girin
4. Cinsiyet seçin ve isminizi girin
5. Ülkelerden birini seçin
6. Bir tarif seçip pişirme modunu test edin

---

## 📞 Yardım Gerekirse

Herhangi bir sorun yaşarsanız:

1. **Terminal'deki hata mesajını** tam olarak kopyalayın
2. Aşağıdaki bilgileri not alın:
   - İşletim sisteminiz (Windows/macOS/Linux)
   - Node.js versiyonunuz: `node -v`
   - Hangi adımda hata aldınız

3. Bana detayları paylaşın, size yardımcı olurum!

---

## ✅ Başarı!

Tebrikler! APK'nızı başarıyla oluşturdunuz. 

**İyi eğlenceler! 👨‍🍳👩‍🍳**

---

## 📚 Ek Kaynaklar

- [Expo Documentation](https://docs.expo.dev/)
- [React Native Docs](https://reactnative.dev/)
- [EAS Build Guide](https://docs.expo.dev/build/introduction/)
- [Android Studio Setup](https://developer.android.com/studio/install)

---

**Not:** Bu proje production-ready değildir. Gerçek kullanım için ek güvenlik ve optimizasyon yapılması önerilir.
