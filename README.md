# Kalkulator Keterampilan & Rekomendasi Drill

Aplikasi web **satu file** untuk membantu merencanakan latihan pemain: menghitung potensi kenaikan mutu (OVR) berdasarkan aturan batas 180%, merekomendasikan drill per posisi, dan menebak kualitas pemain dari pola 7 sesi latihan.

## Ringkasan

- Berjalan sepenuhnya di browser, **tanpa server, tanpa instalasi, tanpa koneksi internet**.
- Semua kode (HTML, CSS, JavaScript) ada di `Drill.html`.
- Bahasa antarmuka: Bahasa Indonesia.

## Cara menjalankan

1. Unduh/`clone` folder ini.
2. Buka `Drill.html` dengan browser (Chrome, Edge, Firefox, atau Safari).
3. Bisa juga diklik dua kali langsung dari File Explorer — tidak perlu menjalankan perintah apa pun.

Perubahan yang kamu buat **tidak disimpan**. Jika halaman disegarkan, aplikasi kembali ke data awal.

## Fitur

### 1. Kalkulator Rule 180% & 15 keterampilan

- Isi nama, posisi, umur, dan OVR awal pemain.
- Atur 15 keterampilan yang dikelompokkan menjadi:
  - Bertahan: Tekel, Penjagaan, Penempatan, Sundulan, Keberanian
  - Menyerang: Umpan, Dribel, Umpan Silang, Tembakan, Penyelesaian
  - Fisik & Mental: Kebugaran, Kekuatan, Agresivitas, Kecepatan, Kreativitas
- Atribut **KUNCI** ditentukan otomatis berdasarkan posisi; atribut di luar daftar posisi ditandai **ABU**.
- Tersedia preset cepat: **Eden Hazard** dan **Albert Fadli**.
- Tabel drill bisa difilter:
  - **Saran Terbaik Untuk Posisi Ini** — minimal 65% atribut drill cocok dengan atribut kunci posisi.
  - **Tampilkan Semua Drill** — seluruh drill dalam database.
- Klik baris drill atau pilih dari dropdown untuk melihat **Bedah Rumus Rule 180%** di panel kanan.

### 2. Roadmap drill berurutan

Panduan latihan satu drill sampai mentok (0% gain), lalu pindah ke drill berikutnya. Tersedia untuk:

- Penyerang (ST / AMC)
- Winger dan gelandang sayap (MR/ML/AML/AMR)
- Bek tengah dan gelandang bertahan (DC / DMC)
- Bek sayap (DR / DL)

Setiap langkah memakai 6 slot drill yang sama.

### 3. Simulator tes kualitas pemain

- Pasang Keahlian Khusus (SA) dengan target 50 poin.
- Latih 7 sesi dengan **Serangan Balik Cepat (Sangat Sulit)** atau **Gym**.
- Klik tombol `+1`, `+2`, atau `+3` sesuai poin yang didapat tiap sesi.
- Aplikasi akan mencocokkan pola 7 sesi dengan 7 tingkat kualitas, dari **Buruk** sampai **Kelas Dunia**.
- Tombol **Reset** mengulang dari awal.

## Cara perhitungan

Untuk sebuah drill:

```text
jumlah atribut aktif (N) = banyaknya atribut yang dilatih drill itu
cap drill               = N × 180%
total saat ini          = jumlah nilai atribut terkait pemain
sisa ruang              = cap − total saat ini
potensi gain            = sisa ÷ 15
OVR maksimum            = OVR awal + potensi gain
```

Jika `sisa <= 0`, drill dianggap **mentok** dan gain bernilai 0%. Aplikasi menampilkan peringatan supaya cendol/booster tidak terbuang.

Nilai `potensi gain` ditampilkan dalam dua bentuk: angka presisi (satu desimal) dan angka bulat yang dipakai untuk OVR akhir.

## Struktur file

```text
.
├── Drill.html   # seluruh aplikasi: tampilan, data drill, dan logika hitung
└── README.md    # dokumentasi ini
```

## Keterbatasan yang diketahui

- **Tidak ada penyimpanan.** Data preset dan hasil hitungan hilang setelah halaman disegarkan. Belum ada fitur ekspor/impor.
- **Kolom umur belum dipakai** dalam perhitungan; nilainya hanya ikut tersimpan di form dan di preset.
- Tombol filter masih bertuliskan **20 Drill**, sementara database `allDrills` berisi **21 entri**. Ini hanya beda teks, bukan kesalahan hitung.
- Ambang rekomendasi `65%` dan pembagian `15%` saat ini ditulis langsung di dalam kode JavaScript.
- Belum ada pengujian otomatis; verifikasi dilakukan dengan membuka halaman dan mencoba tiap tab secara manual.

## Cara mengubah data

Semua data ada di bagian `<script>` dalam `Drill.html`:

- `playerSkills` — nilai 15 keterampilan pemain default.
- `positionKeySkills` — daftar atribut kunci untuk tiap posisi.
- `allDrills` — daftar drill beserta atribut aktif dan tingkat kesulitan.
- `loadPlayerPreset()` — preset pemain.
- `addQualitySeq()` — aturan penentuan tingkat kualitas pemain.

Setelah mengubah kode, segarkan browser untuk melihat hasilnya.
