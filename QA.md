# QA IP Lens — 14 Oktober 2026

## Hasil

23/23 pengujian logika aplikasi lulus (`node tests/qa.mjs`). Harness menjalankan `dist/app.js` asli dengan DOM, clipboard, timer, dan respons jaringan terkontrol; ini bukan tes browser end-to-end.

Cakupan: validasi IPv4/IPv6; auto IP; submit/trim; kedua tombol contoh; refresh; IP sendiri; input invalid; clipboard sukses/ditolak; JSON beserta filename IPv6 dan pembersihan blob; koordinat peta; field opsional; HTTP 429/500; network error; IP privat; respons invalid/JSON rusak; timeout; pencarian bersamaan; input invalid saat request berjalan; referensi aset.

## Browser lokal dan data API asli

- Auto IP berhasil; label hasil IP sendiri benar.
- Lookup 8.8.8.8, 1.1.1.1, IPv6 2606:4700:4700::1111 berhasil.
- Submit dengan Enter, refresh, dan tombol IP sendiri berhasil.
- IP privat 192.168.1.1 ditolak; data sebelumnya dibersihkan dan tombol salin/unduh dinonaktifkan.
- Tombol salin menampilkan keberhasilan dari Clipboard API. Pembacaan ulang melalui clipboard virtual alat QA tidak tersedia, jadi verifikasi isi clipboard OS secara end-to-end belum terkonfirmasi.
- Unduh menghasilkan file nyata `ip-lens-8.8.8.8.json`; JSON berhasil diparse dan IP/organisasi cocok. Event download tool timeout, tetapi file aktual berhasil diverifikasi di Downloads.
- Empat FAQ dapat dibuka/ditutup. Navigasi anchor #lookup, #guide, #privacy benar.
- Link OpenStreetMap menggunakan koordinat hasil, target blank, dan noopener/noreferrer. Klik diuji; tab tujuan eksternal tidak terpapar di alat QA sehingga render peta eksternal belum diverifikasi.
- Logo header/footer berhasil dimuat. Semua favicon, PNG, ICO, manifest, dan SVG mengembalikan HTTP 200 dengan MIME type sesuai.
- Layout 320, 390, 768, dan 1440 px tidak memiliki overflow horizontal. Desktop diperiksa visual.
- Tidak ada error konsol yang terekam pada akhir pengujian.

## Dua bug diperbaiki

1. JSON respons rusak kini menampilkan pesan Bahasa Indonesia yang jelas, bukan exception teknis.
2. Input invalid membatalkan request berjalan dan menaikkan request serial, sehingga respons lama tidak menimpa pesan validasi. Kontrol loading dipulihkan.

## Batas verifikasi

Error API, offline, timeout, dan balapan request diuji secara deterministik dalam harness, bukan dengan mengganggu jaringan pengguna. Pengujian dilakukan lokal melalui browser aplikasi, bukan seluruh browser/OS atau deployment Vercel. Rendering favicon di tab OS dan instalasi ikon PWA di perangkat asli belum diuji. Layanan API eksternal tetap bergantung pada ketersediaan dan kuota penyedia.
