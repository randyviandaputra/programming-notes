# Cara Build App Bundle dengan Flutter

## Daftar Isi
- [App Bundle](#intro)
- [Mengapa App Bundle](#mengapa-app-bundle)
- [Build App Bundle](#build-app-bundle)
- [Kesimpulan](#kesimpulan)

## App Bundle
<a name="intro"></a>
App Bundle merupakan format distribusi yang baru dan lebih efisien untuk membuat dan merelease suatu aplikasi. App Bundle mulai dikenalkan oleh Google pada tahun 2018.

## Mengapa App Bundle
<a name="mengapa-app-bundle"></a>
- App Bundle memiliki ukuran yang lebih kecil dibandingkan APK.
- Memiliki user experience yang lebih baik untuk pengguna, karena App Bundle menyediakan apa yang benar-benar dibutuhkan. Seperti ukuran density, bahasa, resources.
- Apabila pengembangan aplikasi menggunakan modular App Bundle sangat menguntungkan, dapat melakukan kostumisasi feature delivery.

## Build App Bundle
<a name="build-app-bundle"></a>
Pertama, siapkan project aplikasi Flutter yang akan kamu build. Kamu dapat menggunakan Android Studio ataupun Visual Studio Code.

### Membuat keystore
Untuk Mac / Linux, ketik perintah berikut di terminal :
```
keytool -genkey -v -keystore ~/nama_file_.jks -keyalg RSA -keysize 2048 -validity 10000 -alias key
```
Untuk Windows, gunakan perintah berikut :
```
keytool -genkey -v -keystore c:/Users/USER_NAME/nama_file.jks -storetype JKS -keyalg RSA -keysize 2048 -validity 10000 -alias key
```
Kemudian tekan enter, ikuti langkah-langkah berikut :
1. Masukan keystore password
2. Masukan password konfirmasi
3. Masukan nama depan dan nama belakang
4. Masukan unit organisasi
5. Masukan nama organisasi
6. Masukan nama kota
7. Masukan negara atau provinsi
8. Masukan 2 huruf dari kode negara asal
9. Jika sudah yakin ketik yes, jika belum ketik no
10. Tunggu beberapa saat, maka file keystore sudah berhasil dibuat

### Note
Untuk keystore simpan ditempat yang aman, jangan sampai hilang. Karena apabila kalian lupa atau keystorenya hilang maka aplikasi yang kamu release tidak bisa diupdate lagi.

### Integrasi keystore
Buat file baru bernama key.properties didalam folder project_kamu/android/key.properties. Kemudian isi seperti berikut :
```
storePassword= Masukan password store sebelumnya
keyPassword= Masukan password key sebelumnya
keyAlias= Masukan keyAlias
storeFile= Masukan lokasi file keystore, contoh User/file/key.jks
```

### Konfigurasi gradle
Buka project_flutter/android/app/build.gradle

Tambahkan kode berikut sebelum android { }
```
def keystoreProperties = new Properties()
def keystorePropertiesFile = rootProject.file('key.properties')
if (keystorePropertiesFile.exists()) {
    keystoreProperties.load(new FileInputStream(keystorePropertiesFile))
}
```

Tambahkan dan ubah pada bagian buildTypes { } menjadi seperti berikut :
```
signingConfigs {
    release {
        keyAlias keystoreProperties['keyAlias']
        keyPassword keystoreProperties['keyPassword']
        storeFile file(keystoreProperties['storeFile'])
        storePassword keystoreProperties['storePassword']
    }
}
buildTypes {
    release {
        signingConfig signingConfigs.release
        minifyEnabled true
        useProguard true
        proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
    }
}
```

### Menambahkan Proguard
Secara default, Flutter tidak mengamankan dan melakukan minify. Untuk meningkatkan keamanan aplikasi yang akan kita release perlu ditambahkan konfigurasi proguard. Sehingga kode sumber aplikasi yang tergenerate disamarkan.

Buat file baru pada folder android/app/proguard-rules.pro. Tambahkan kodenya seperti berikut :
```
## Flutter wrapper
-keep class io.flutter.app.** { *; }
-keep class io.flutter.plugin.**  { *; }
-keep class io.flutter.util.**  { *; }
-keep class io.flutter.view.**  { *; }
-keep class io.flutter.**  { *; }
-keep class io.flutter.plugins.**  { *; }
-dontwarn io.flutter.embedding.**
-dontwarn android.**
```

### Konfigurasi Manifest
Sebelum release aplikasi kamu, pastikan file AndroidManifest.xml pada folder android/app/src/main dan cek seperti label, icon, permission. Untuk menambahkan permission internet, tambahkan kode berikut didalam file AndroidManifest 

```
<uses-permission android:name="android.permission.INTERNET"/>
```

### Build app bundle
Sebelumnya saya sarankan kamu sudah update Flutter versi terbaru, karena versi lama untuk build App Bundle belum support untuk split app-armeabi-v7a dan app-arm64-v8a.

Jika kamu ingin build app bundle yang otomatis versi armeabi-v7a dan arm64, gunakan perintah berikut di terminal :

- Mode release :
```
flutter build appbundle --release
```
- Mode debug :
```
flutter build appbundle --debug
```

Jika kamu ingin memisahkan hanya untuk sistem yang spesifik, gunakan perintah seperti berikut contohnya :
```
flutter build appbundle --release --target-platform=android-arm
```

Tunggu sampai proses build app bundle selesai. Untuk mengecek file hasil generate, dapat dilihat pada folder :

Release :
project/build/app/outputs/bundle/release

Debug : project/build/app/outputs/bundle/

## Kesimpulan
<a name="kesimpulan"></a>
App Bundle sangat direkomendasikan oleh Google ketika kamu ingin release aplikasi ke Playstore.

Tentunya catatan ini akan update lagi kedepannya, jangan lupa untuk share. Semoga bermanfaat ya 😃