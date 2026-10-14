# IP Lens

Website pengecekan IP dalam bahasa Indonesia. HTML, CSS, dan JavaScript tanpa framework atau build.

## Fitur

- Deteksi IP publik dari koneksi browser.
- Pencarian IPv4 dan IPv6 dengan validasi format.
- Informasi organisasi/ISP, ASN, zona waktu, dan perkiraan lokasi.
- Salin IP, unduh JSON, serta tautan OpenStreetMap.
- Tampilan responsif, penanganan timeout dan error API.

## Menjalankan lokal

```sh
python3 -m http.server 4173 --directory dist
```

Buka http://localhost:4173.

## Deploy ke Vercel

1. Import repository `ganoolmovie5th-cell/ip-lens-gpt`.
2. Pilih branch `main` dan Root Directory `.`.
3. Framework Preset: **Other**. Tidak diperlukan install atau build command.
4. Output Directory: **dist** (sudah diatur di `vercel.json`).
5. Klik Deploy. Tidak ada environment variable wajib.

## Sumber data dan batasan

Browser mengirim permintaan langsung ke API HTTPS `ipwho.is`. Tidak ada API key maupun riwayat pencarian yang disimpan aplikasi. Data lokasi merupakan perkiraan, bukan GPS atau alamat rumah. API pihak ketiga memiliki batas penggunaan dan ketentuan layanan; tinjau paket dan ketentuannya sebelum penggunaan komersial atau trafik tinggi. Google Fonts memuat font dan OpenStreetMap hanya dibuka ketika tautan peta diklik.

## Verifikasi

`node --check dist/app.js` memeriksa sintaks JavaScript. Versi awal telah diuji di browser untuk IP otomatis, lookup IPv4/IPv6, input tidak valid, serta tampilan ponsel.

## Regression QA

Jalankan `node tests/qa.mjs` (Node.js 18+). Tidak memerlukan instalasi dependensi atau akses jaringan. Lihat `QA.md` untuk cakupan tes browser nyata dan batas verifikasi.
