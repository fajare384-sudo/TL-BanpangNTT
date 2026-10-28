# Pemantauan Tindak Lanjut Gagal Salur & Retur Beras Bantuan Pangan NTT

Dashboard publik untuk memantau tindak lanjut dan konfirmasi temuan gagal salur dan retur beras Bantuan Pangan Juli–September 2026 di NTT, oleh **Inspektorat Badan Pangan Nasional**.

Pihak yang dipantau: Dinas Ketahanan Pangan Kab/Kota, Dinas Ketahanan Pangan Provinsi, Transporter (JPL), dan Perum BULOG. Jendela pemantauan **H+7** dihitung dari `meta.t0` di `data/tindak-lanjut.json` (saat ini 28 Okt 2026, berakhir 4 Nov 2026).

> Angka adalah indikasi untuk konfirmasi, bukan kesimpulan pelanggaran. Keputusan tolak/koreksi berada pada reviu APIP dan pimpinan.

## Isi repositori

```
index.html                  Halaman dashboard (satu berkas, tanpa dependensi)
data/tindak-lanjut.json     Data butir, status, jawaban, dan tautan bukti
bukti/                      Berkas bukti yang ditayangkan: bukti/<kode butir>/<berkas>
.nojekyll                   Agar GitHub Pages menyajikan berkas apa adanya
README.md                   Panduan ini
```

## Cara mengunggah ke GitHub

### Opsi A: lewat browser (tanpa Git)
1. Buat akun di [github.com](https://github.com), lalu **New repository** (mis. `pemantauan-gagal-salur-ntt`), pilih **Public**.
2. Di halaman repositori, klik **Add file → Upload files**.
3. Seret **isi** folder ini (`index.html`, `data`, `bukti`, `.nojekyll`, `README.md`), bukan folder induknya. Klik **Commit changes**.
   - Berkas `.nojekyll` bisa tersembunyi di pemilih berkas; bila tidak terunggah, abaikan, situs tetap berjalan.
   - Folder `bukti` kosong tidak ikut terunggah oleh browser. Buat otomatis saat mengunggah bukti pertama.

### Opsi B: lewat Git
```bash
cd gagal-salur-monitor
git init -b main
git add .
git commit -m "Dashboard pemantauan tindak lanjut gagal salur NTT"
git remote add origin https://github.com/<akun>/<repositori>.git
git push -u origin main
```

### Mengaktifkan GitHub Pages
1. **Settings → Pages**.
2. **Source:** Deploy from a branch. **Branch:** `main`, folder `/ (root)`. Klik **Save**.
3. Tunggu 1–2 menit. Alamat publik: `https://<akun>.github.io/<repositori>/`.

## Memperbarui status (Admin APIP)
1. Buka `https://<akun>.github.io/<repositori>/?admin=1`.
2. Per butir: ubah status, isi ringkasan jawaban, tautan/path bukti, dan centang **Tayangkan** bila boleh dilihat publik.
3. Klik **Unduh JSON** pada bilah atas.
4. Ganti `data/tindak-lanjut.json` di repositori dengan berkas hasil unduhan, lalu **Commit**.
5. Untuk bukti yang ditayangkan, unggah berkasnya ke `bukti/<kode butir>/` (mis. `bukti/T-01/stok-opname.pdf`) dan isi path itu di kolom bukti.

Draf perubahan tersimpan sementara di peramban Admin sampai JSON di-commit. Jawaban dan bukti hanya tampil ke publik bila ditandai **Tayangkan**.

## Unggah bukti oleh pihak terkait
Setiap butir punya tombol **Unggah** pada berkas yang diminta. File terkirim sebagai lampiran email ke `fajare384@gmail.com` lewat [FormSubmit](https://formsubmit.co), tanpa server sendiri.

1. **Aktivasi sekali:** setelah situs tayang, kirim satu uji coba. FormSubmit akan mengirim email aktivasi ke alamat tujuan; klik tautan konfirmasinya. Sebelum itu, berkas tidak akan masuk.
2. **Sembunyikan alamat email (disarankan):** setelah aktivasi, FormSubmit memberi alias acak. Di `index.html`, ganti nilai `UPLOAD_EMAIL` dengan alias itu agar alamat tidak terbaca di kode publik.
3. Batas: 8 MB per berkas; jenis pdf, jpg, png, doc, docx, xls, xlsx, zip. Unggah ditutup otomatis setelah H+7.
4. Berkas tidak disimpan di situs maupun oleh FormSubmit. Simpan lampiran dari email.
5. Status di halaman **tidak berubah otomatis** setelah unggah; Admin APIP memperbaruinya (langkah di atas).

## Mengubah tanggal H+0 / jendela pemantauan
Ubah `meta.t0` (format `YYYY-MM-DD`) dan `meta.jendela_hari` di `data/tindak-lanjut.json`. Tenggat tiap butir (H+3, H+5, H+7) mengikuti otomatis.

Untuk menguji tampilan pada tanggal lain, tambahkan `?today=2026-11-01` pada alamat.

## Keamanan dan privasi
- `?admin=1` hanya membuka antarmuka penyuntingan, **bukan autentikasi**. Pengendali sebenarnya adalah hak commit: aktifkan **branch protection** dan batasi akses tulis hanya untuk Admin APIP.
- Semua isi repositori publik dapat dibaca siapa saja. Jangan commit bukti berisi data pribadi (NIK, rekening, nama PBP).
- Detail butir yang masih dalam reviu (T-12 dan D-09) sengaja tidak ada di repositori. Berkas `butir-internal.json` dipegang APIP dan diimpor lewat mode Admin di komputer lokal; **jangan diunggah**.
- Halaman unggah bisa diakses siapa saja yang membuka situs; perlindungan hanya berupa batas ukuran/jenis file dan jebakan spam sederhana.

## Sumber data
- Analisis Transporter 7 Kab. Flores (verifikasi dokumen 22 Okt 2026; data gagal salur 18 Okt 2026)
- Analisis Non-Transporter 7 Kab. Flores
- Catatan dokumen pada paparan cross-check (27 Okt 2026)

## Lisensi
Tentukan sendiri sebelum dipublikasikan (mis. CC BY 4.0 untuk data). Tambahkan berkas `LICENSE` bila diperlukan.
