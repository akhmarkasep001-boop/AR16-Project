# AR16 OS — Studio Konten Affiliate (Android WebView)

Paket sumber Android untuk membungkus antarmuka HTML ke aplikasi Android. Target: bisa dibuka di Android Studio/cloud build dari HP.

## Status penting
- Ini **proyek sumber**, bukan APK yang sudah dikompilasi.
- Bagian penyusun prompt dan salin prompt berfungsi di HTML demo.
- Bagian render video sengaja diberi label **belum aktif**. Tidak ada API video yang dipanggil dan tidak ada video AI sungguhan yang dihasilkan.
- `app/src/main/assets/index.html` adalah antarmuka HTML yang disertakan. Jika punya HTML asli lengkap dari Gemini Canvas, salin seluruh kode tersebut ke file ini untuk mempertahankan tampilan persis aslinya. Simpan salinan cadangan terlebih dahulu.
- API key tidak boleh ditanam di HTML atau APK.

## Cara build dari HP Android (ringkas)
1. Unduh dan ekstrak ZIP ini.
2. Buka layanan IDE/build Android berbasis cloud yang mendukung proyek Gradle Android, atau pindahkan folder ini ke komputer yang menjalankan Android Studio.
3. Buka folder proyek `AR16_OS_Android_Source`.
4. Build varian `debug` untuk menghasilkan APK uji.
5. Unduh APK hasil build ke HP, lalu izinkan pemasangan dari sumber yang digunakan bila Android memintanya.

Build APK membutuhkan lingkungan Android/Gradle yang sesuai. ZIP ini sendiri belum berupa APK.

## Penggantian HTML dengan versi asli
File target: `app/src/main/assets/index.html`

Jangan menghapus JavaScript bridge `AndroidApp` jika nanti ditambahkan integrasi native; saat ini HTML tidak membutuhkan bridge untuk fungsi dasarnya. WebView sudah mendukung pemilih file gambar lewat `WebChromeClient`.

## Isi
- `app/src/main/assets/index.html` — antarmuka demo dan penyusun prompt
- `app/src/main/java/com/ar16/studiokonten/MainActivity.java` — Activity WebView, izin file chooser, tombol back
- `app/src/main/AndroidManifest.xml`
- Gradle project files


## Build APK dari HP menggunakan GitHub Actions
File workflow sudah disediakan di `.github/workflows/android.yml`.

1. Buat repository baru di GitHub melalui browser HP.
2. Unggah semua isi folder proyek (termasuk folder `.github`) ke repository. Pastikan `settings.gradle`, `build.gradle`, `gradle.properties`, dan folder `app` berada di root repository, bukan di dalam folder tambahan.
3. Buka tab **Actions** pada repository. Jika diminta, aktifkan Actions.
4. Pilih workflow **Build AR16 OS APK**, lalu tekan **Run workflow**. Atau workflow berjalan otomatis setelah push ke branch `main`.
5. Setelah selesai dengan status hijau, buka run tersebut, cari bagian **Artifacts**, lalu unduh `AR16-OS-debug-APK`.
6. Ekstrak ZIP artifact yang diunduh; file APK ada di dalamnya. Ketuk APK untuk memasang dan ikuti peringatan Android bila muncul.

GitHub Actions menyediakan kuota penggunaan yang bergantung pada jenis akun dan repository. Jangan unggah API key atau rahasia ke repository. Build workflow ini membuat APK debug untuk pengujian, bukan rilis Play Store.
