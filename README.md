# BA Sell Out Performance Dashboard (GitHub Pages)

Situs statis: `index.html` (halaman password) + `dashboard.enc` (dashboard terenkripsi AES-256).
Dashboard asli tidak ada di repo ini dalam bentuk terbaca.

## Struktur
```
/
├─ index.html                 ← halaman Enter Password + loader (jangan diubah untuk ganti password)
├─ dashboard.enc              ← dashboard terenkripsi (diganti saat update data / ganti password)
├─ .nojekyll                  ← agar GitHub Pages menyajikan file apa adanya
├─ .gitignore
├─ README.md
└─ tools/
   ├─ encrypt.html            ← ganti password / update data, langsung di browser (tanpa install)
   └─ encrypt_dashboard.py    ← alternatif via Python
```

## Deploy (sekali saja)
1. GitHub → **New repository** → nama bebas (saran: nama yang tidak mudah ditebak) → **Public** → Create.
2. **Add file → Upload files** → seret SEMUA isi folder ini (termasuk folder `tools` dan file `.nojekyll`) → **Commit changes**.
3. **Settings → Pages → Build and deployment → Source: Deploy from a branch → Branch: `main` / `(root)` → Save.**
4. Tunggu 1–3 menit. Link: `https://<username>.github.io/<nama-repo>/`

## Ganti password (tanpa mengubah dashboard)
1. Siapkan file dashboard `.html` asli (yang tidak terenkripsi) di komputer Anda.
2. Buka `tools/encrypt.html` (klik dua kali dari komputer, atau buka dari link Pages) → pilih file → isi password baru 2x → unduh `dashboard.enc`.
3. Di repo: **Add file → Upload files** → upload `dashboard.enc` baru (nama sama, menimpa) → Commit.
4. Selesai. Link tetap sama; password lama tidak berlaku lagi.

## Update data bulan depan
Sama persis dengan "Ganti password": enkripsi dashboard HTML baru (boleh dengan password yang sama), lalu timpa `dashboard.enc`.

## Penting soal keamanan
Ini perlindungan sisi-browser untuk situs statis, bukan kontrol akses server.
- Isi dashboard terenkripsi (AES-256-GCM, kunci dari password via PBKDF2 600.000 iterasi), jadi tanpa password isinya tidak terbaca.
- Namun file `dashboard.enc` bisa diunduh siapa pun yang tahu link, lalu ditebak passwordnya secara offline. Kekuatan password = kekuatan perlindungan. Pakai passphrase panjang (4+ kata acak + angka).
- Siapa pun yang tahu password dapat membukanya, dan tidak ada log siapa yang masuk. Ganti password bila ada yang tidak lagi berhak.
- Jangan pernah meng-upload file dashboard `.html` asli ke repo ini.
