# Tugasku

Aplikasi Android sederhana untuk mengelola tugas kuliah: buat daftar tugas, atur tenggat, tambah deskripsi, dan gunakan pengingat (notifikasi) agar tidak terlewat deadline.

## Fitur

- **Manajemen tugas**
  - Tambah tugas (judul, mata kuliah, tenggat, deskripsi)
  - Edit & hapus tugas
  - Tandai tugas selesai (dipisah menjadi tab **Aktif** dan **Selesai**)
- **Lampiran**
  - Lampirkan gambar (disimpan ke internal storage aplikasi)
  - Lampirkan file dokumen (PDF/DOC/DOCX/XLS/XLSX/PPT/PPTX) via Storage Access Framework
  - Tambah link (mis. Google Drive)
  - Buka lampiran/link langsung dari aplikasi
- **Pengingat tenggat (notifikasi)**
  - Pengingat dijadwalkan menggunakan `AlarmManager`
  - Jarak pengingat bisa diatur (30 menit / 1 jam / 1 hari sebelum tenggat)
- **Tema**
  - Mode gelap & mode terang
- **Splash screen + lokasi**
  - Meminta izin lokasi untuk menampilkan lokasi (jika tersedia)
  - Mengatur bahasa/locale aplikasi berdasarkan country code yang terdeteksi

## Tech Stack

- **Android** (XML Views)
- **Bahasa**: Java
- **Build system**: Gradle (Kotlin DSL)
- **UI**: AndroidX AppCompat, Material Components, RecyclerView
- **Lokasi**: Google Play Services Location (`play-services-location`)
- **Penyimpanan data**: `SharedPreferences` (JSON)

## Requirement

- **Android Studio** terbaru
- **JDK** 11 (sesuai konfigurasi `compileOptions`)
- **Min SDK**: 26
- **Compile/Target SDK**: 36

## Cara Menjalankan

1. **Clone repository**

   ```bash
   git clone <url-repo-kamu>
   ```

2. **Buka di Android Studio**

   - `File` -> `Open` -> pilih folder `Tugasku`

3. **Sync Gradle**

   - Tunggu proses *Gradle Sync* selesai

4. **Jalankan aplikasi**

   - Pilih device/emulator
   - Klik **Run** (Shift+F10)

## Build APK

- Debug APK:

  ```bash
  ./gradlew assembleDebug
  ```

- Release APK (konfigurasi signing dibutuhkan jika ingin rilis):

  ```bash
  ./gradlew assembleRelease
  ```

Output APK biasanya berada di:

- `app/build/outputs/apk/debug/`
- `app/build/outputs/apk/release/`

## Permission yang Digunakan

Aplikasi membutuhkan beberapa permission berikut:

- **Notifikasi**: `POST_NOTIFICATIONS` (Android 13+)
- **Lokasi**: `ACCESS_FINE_LOCATION`, `ACCESS_COARSE_LOCATION` (untuk menampilkan lokasi di splash screen dan menentukan country/locale)
- **Internet**: `INTERNET` (dibutuhkan untuk beberapa komponen/fitur yang membuka link)
- **Akses gambar**:
  - Android 13+: `READ_MEDIA_IMAGES`
  - Android <= 12: `READ_EXTERNAL_STORAGE` (dibatasi `maxSdkVersion=32`)

Catatan: akses file lampiran menggunakan **Storage Access Framework** (`ACTION_OPEN_DOCUMENT`), sehingga user memilih file secara manual dari penyimpanan.

## Struktur Proyek (ringkas)

- **`app/src/main/java/com/example/tugasku/`**
  - `SplashActivity` — splash + lokasi + pengaturan locale
  - `MainActivity` — daftar tugas aktif/selesai, menu, tema, dan pengaturan jarak pengingat
  - `AddTaskActivity` — tambah tugas + lampiran
  - `EditTaskActivity` — edit/hapus/selesaikan tugas + lampiran
  - `PreviewTaskActivity` — pratinjau detail tugas
  - `TaskManager` — simpan/muat data tugas via `SharedPreferences` (JSON)
  - `ReminderScheduler` + `DeadlineReceiver` — jadwal & trigger notifikasi pengingat
  - `ThemeManager` — simpan preferensi tema

## Catatan Penting

- Data tugas disimpan lokal menggunakan `SharedPreferences` (format JSON). Belum menggunakan database (Room/SQLite).
- Menu **Ekspor Data** saat ini masih placeholder.

## Kontribusi

Pull request dan issue sangat dipersilakan:

1. Fork repository
2. Buat branch fitur (`feature/nama-fitur`)
3. Commit perubahan
4. Ajukan Pull Request

## License

Belum ditentukan. Tambahkan file `LICENSE` jika ingin menggunakan lisensi tertentu (mis. MIT).
