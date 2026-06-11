---
title: "Mate Harian"
description: "Latihan matematika dengan pengulangan berjarak untuk iPhone dan iPad"
---

# Kebijakan Privasi — Mate Harian

**Tanggal berlaku:** 2026-05-21
**Terakhir diperbarui:** 2026-06-10

Kebijakan ini menjelaskan bagaimana aplikasi iOS Mate Harian ("Aplikasi") menangani informasi Anda. Berlaku sejak v1.0 dan seterusnya, termasuk model berbagi CloudKit satu keluarga pada v3 (yang menggantikan berbagi per profil pada v2.0).

## Ringkasan dengan bahasa sederhana

- Kami tidak menjalankan server apa pun. Kami tidak mengumpulkan informasi pribadi apa pun.
- Semuanya tetap di perangkat Anda kecuali Anda menyalakan **sinkronisasi iCloud**; dalam hal itu Apple, bukan kami, yang menyimpannya di akun iCloud pribadi Anda.
- Aplikasi memakai mikrofon hanya saat Anda menjawab soal dalam mode suara. Audio diproses oleh pengenalan ucapan Apple (di perangkat, kelas Siri) dan langsung dibuang; kami tidak pernah menyimpan, mengunggah, atau menganalisisnya.
- Tidak ada pelacak pihak ketiga, iklan, atau SDK analitik.

## Yang Aplikasi simpan di perangkat Anda

- **Profil.** Nama, emoji, warna, dan pengaturan per profil.
- **Status pengulangan berjarak.** Untuk tiap kartu (mis. `7 + 8`): tanggal tinjauan berikutnya yang dijadwalkan, kesulitan, stabilitas, dan jumlah tinjauan.
- **Aktivitas.** Hitungan harian tinjauan yang selesai per profil (dipakai untuk chip rentetan dan layar Statistik).
- **Kesalahan.** Antrean soal yang baru saja Anda jawab salah, agar Aplikasi dapat menampilkannya kembali.
- **Preferensi.** Sakelar seluruh Aplikasi, seperti apakah sinkronisasi iCloud menyala.

Semua ini ditulis ke folder Dokumen tersendiri yang terisolasi milik Aplikasi dan ke `UserDefaults`. Aplikasi tidak dapat membaca data aplikasi lain, dan aplikasi lain tidak dapat membaca data Aplikasi.

## Yang Aplikasi simpan secara opsional di iCloud

Sinkronisasi iCloud **mati secara bawaan**. Saat Anda menyalakannya (ikon roda gigi → **Pengaturan → Sinkronisasi → Gunakan iCloud**), Aplikasi menulis data yang sama seperti dijelaskan di atas ke iCloud pribadi Anda melalui API **CloudKit** Apple. Ini iCloud Anda, hanya dapat diakses oleh Anda di perangkat yang masuk dengan ID Apple yang sama. Kami tidak memiliki akses ke sana.

- Data yang persis disinkronkan: profil, status kartu, aktivitas, kesalahan, dan (opsional) metadata berbagi keluarga (nama tampilan yang Anda pilih untuk keluarga Anda).
- Sinkronisasi iCloud **tidak** mencakup isi rekaman suara apa pun atau analitik apa pun.
- Saat Anda masuk dengan ID Apple yang berbeda, Aplikasi mendeteksi perubahan dan mematikan sinkronisasi sampai Anda menyalakannya lagi secara eksplisit, agar data tidak diam-diam terunggah ke akun lain.
- Menghapus profil dari **Kelola Profil** membuang profil dari perangkat dan (saat iCloud dapat dijangkau pada ID Apple asal) dari salinan iCloud Anda juga.

## Berbagi keluarga

Di v3, berbagi terjadi pada tingkat **keluarga**, bukan per profil. Buka ikon roda gigi → **Pengaturan → Keluarga → Siapkan keluarga**, beri nama keluarga Anda, dan undang anggota keluarga melalui lembar berbagi iOS standar (Pesan, Mail, atau AirDrop).

- Semua profil di perangkat pemilik termasuk dalam keluarga. Mengundang seorang anggota keluarga membagikan semuanya sekaligus.
- Data berada di **iCloud pemilik keluarga**. Peserta tidak menyimpan salinan terpisah di iCloud mereka sendiri; aktivitas belajar mereka ditulis langsung ke CloudKit pemilik melalui model izin CKShare bercakupan zona milik Apple.
- Bergabung dengan keluarga bersifat **permanen di perangkat yang bergabung**: profil lokal peserta yang ada diganti dengan profil keluarga. Sebelum bergabung, Aplikasi menawarkan opsi **Ekspor profil ke berkas** agar Anda menyimpan salinan JSON data Anda saat ini dan mengimpornya kembali nanti jika berubah pikiran.
- Jika pemilik membubarkan keluarga (Pengaturan → Keluarga → Bubarkan) atau keluar dari iCloud, peserta kehilangan akses langsung pada sinkronisasi berikutnya. Cache lokal profil keluarga menjadi milik mereka sendiri (tanpa penghapusan permanen saat keluar).
- Peserta dapat meninggalkan keluarga kapan saja (Pengaturan → Keluarga → Tinggalkan). Saat keluar, ia menyimpan profil keluarga di perangkatnya sebagai miliknya sendiri.
- Batas `CKShare` Apple adalah 100 peserta per item berbagi. Skala keluarga yang wajar adalah ~6.

## Ekspor / Impor (cadangan JSON)

Di **Pengaturan → Cadangan** Anda bisa:

- **Ekspor profil ke berkas**: menyimpan berkas JSON berisi semua profil di perangkat saat ini (apa pun status keluarganya). Berguna sebagai cadangan manual atau sebelum operasi permanen.
- **Impor profil dari berkas**: memulihkan ekspor sebelumnya. Mode **Gabungkan** menambahkan profil yang hilang dan memperbarui yang ada jika salinan yang diimpor lebih baru. Mode **Ganti** menghapus profil lokal dan memasang kumpulan yang diimpor; hanya tersedia saat Anda tidak sedang dalam keluarga.

## Mikrofon dan pengenalan ucapan

Saat mode suara menyala, ketika Anda menjawab soal, Aplikasi:

1. Menangkap audio mikrofon langsung dengan `AVAudioEngine`.
2. Mengalirkannya ke `SFSpeechRecognizer` (kerangka kerja Apple). Pada perangkat iOS modern, pengenalan berjalan di perangkat secara bawaan; sebagian konfigurasi mungkin memakai server pengenalan ucapan Apple.
3. Membaca digit yang ditranskripsikan dan menilai jawaban.
4. Menghentikan penangkapan begitu jawaban akhir diperoleh.

Kami tidak menyimpan audio, transkrip, atau sinyal turunan apa pun. Kami tidak mengirimkan audio ke pihak mana pun selain `SFSpeechRecognizer` Apple. Aplikasi meminta `NSMicrophoneUsageDescription` dan `NSSpeechRecognitionUsageDescription` saat pertama dipakai; jika salah satu izin ditolak, mode suara otomatis dinonaktifkan dan papan tombol angka di layar dipakai.

## Log diagnostik

Aplikasi mengeluarkan peristiwa diagnostik tak terstruktur melalui kerangka kerja `OSLog` standar Apple (mis. "sesi belajar berakhir, benar=12 salah=3"). Log ini:

- Tetap di perangkat.
- Hanya terlihat oleh Anda, di Console.app saat perangkat tersambung ke Mac.
- Memakai klasifikasi privasi `.private` Apple untuk nilai yang berpotensi mengidentifikasi (id profil, nama profil), sehingga nilai-nilai itu disensor pada build yang dirilis.

Kami tidak mengumpulkan, mengambil, atau mengirimkan isi `OSLog`.

## Data yang TIDAK kami kumpulkan

- Nama, email, atau info kontak Anda.
- Lokasi Anda.
- Pengidentifikasi perangkat apa pun (IDFA, IDFV, id iklan).
- Laporan kerusakan melebihi yang mungkin dikumpulkan Apple melalui pengaturan iOS Anda.
- Analitik atau telemetri perilaku apa pun.
- Informasi pembayaran atau penagihan (pembelian sepenuhnya ditangani oleh Apple).

## Privasi anak

Mate Harian dirancang agar aman untuk anak-anak. Karena Aplikasi tidak mengumpulkan informasi pribadi dan tidak menghubungi pihak ketiga, ia memenuhi definisi "tanpa informasi pribadi" dari COPPA. Kami tidak menampilkan iklan, dan tidak ada akun atau fitur sosial. Mate Harian menyertakan satu pembelian dalam aplikasi sekali bayar (buka kunci aplikasi lengkap); karena aplikasi dirancang untuk anak-anak, gerbang dewasa ditampilkan sebelum pembelian apa pun, sebagaimana disyaratkan aturan kategori Anak-anak Apple. Semua pembayaran dan penukaran kode apa pun ditangani oleh Apple melalui App Store. Aplikasi tidak pernah melihat atau menyimpan detail pembayaran Anda.

## Pilihan Anda

- **Matikan mode suara** kapan saja per profil (Pengaturan → Mode suara), atau secara global dengan menolak izin mikrofon di pengaturan iOS.
- **Matikan sinkronisasi iCloud** kapan saja (ikon roda gigi → Pengaturan → Sinkronisasi → Gunakan iCloud → mati). Mematikannya tidak menghapus salinan iCloud; hapus tiap profil satu per satu jika ingin membuangnya.
- **Bubarkan atau tinggalkan keluarga** (Pengaturan → Keluarga → Bubarkan / Tinggalkan) untuk berhenti berbagi. Membubarkan mencabut akses peserta ke keluarga Anda; meninggalkan menyimpan profil keluarga di perangkat Anda sebagai milik Anda sendiri.
- **Ekspor profil ke berkas** (Pengaturan → Cadangan → Ekspor) dan menyimpannya secara lokal — cadangan manual yang tidak pernah menyentuh iCloud.
- **Atur ulang progres profil** tanpa menghapus profil (pengaturan profil → Atur Ulang).
- **Hapus profil** (Kelola Profil → geser atau ketuk untuk menghapus) — juga membuang salinan iCloud saat sinkronisasi menyala. Ulangi per profil untuk membuang semuanya.

## Perubahan kebijakan ini

Jika kami mengubah kebijakan ini, versi baru akan tersedia di URL yang sama dengan tanggal **Terakhir diperbarui** yang diperbarui. Perubahan penting juga akan dicatat dalam catatan rilis Aplikasi.

## Kontak

Pertanyaan tentang kebijakan ini atau data Anda? Email **spacedmath@gmail.com**.
