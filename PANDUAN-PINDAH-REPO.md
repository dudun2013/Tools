# Panduan Menyalin Proyek ke GitHub Sendiri

Panduan ini digunakan untuk mengelola salinan proyek dari repositori sumber ke repositori GitHub milik sendiri, tanpa mengubah repositori sumber.

## 1. Masuk ke folder proyek

```powershell
cd C:\Users\user\Desktop\Tools\NamaProyek
```

## 2. Periksa kondisi Git

```powershell
git status
git remote -v
git ls-files
Get-ChildItem -Force
```

Periksa file yang akan dipublikasikan. Jangan ikut mengunggah token, kata sandi, file `.env`, data pribadi, atau hasil lokal yang sensitif.

## 3. Buat `.gitignore`

Sesuaikan dengan jenis proyek. Contoh untuk Python:

```gitignore
__pycache__/
*.py[cod]
.env
.env.*
!.env.example
.venv/
venv/
outputs/logs/
```

Tambahkan pola lain sesuai file lokal proyek. `.gitignore` tidak menghapus file yang sudah pernah masuk ke riwayat Git.

## 4. Keluarkan file lokal dari pelacakan Git

Jika file cache atau log sudah dilacak Git, gunakan perintah yang sesuai dengan folder proyek, misalnya:

```powershell
git rm -r --cached -- path\ke\cache
```

Untuk folder log:

```powershell
git rm -r --cached -- outputs/logs
```

Periksa status sebelum melakukan commit. Opsi `--cached` mengeluarkan file dari pelacakan Git tanpa sengaja menghapus salinan lokalnya.

## 5. Simpan perubahan

```powershell
git add .gitignore
git status
git commit -m "Add gitignore and remove generated files"
```

Jika perubahan lain memang diperlukan, tambahkan hanya file yang sudah diperiksa.

## 6. Buat repositori tujuan

Buat repositori baru di akun GitHub sendiri. Jika akan melakukan push atas riwayat lokal yang sudah ada, buat repositori tujuan kosong tanpa README, `.gitignore`, atau lisensi tambahan.

## 7. Atur remote

Contoh untuk repositori sumber `YogaRmdn/Flag`:

```powershell
git remote set-url origin https://github.com/USERNAME/Flag.git
git remote add upstream https://github.com/YogaRmdn/Flag.git
git remote -v
```

Ganti `USERNAME`, nama proyek, dan URL upstream sesuai proyek yang sedang dikelola.

Jika `upstream` sudah ada, jangan menambahkannya lagi. Periksa dengan `git remote -v` terlebih dahulu.

## 8. Periksa sebelum push

```powershell
git status
git log -3 --oneline
```

Pastikan `origin` menunjuk ke repositori milik sendiri dan `upstream` menunjuk ke sumber yang benar.

## 9. Unggah ke repositori sendiri

Jika repositori tujuan kosong dan branch lokal bernama `main`:

```powershell
git push -u origin main
```

Jangan push jika alamat remote belum benar atau isi yang akan dipublikasikan belum diperiksa.

## 10. Verifikasi

Buka repositori tujuan di GitHub dan pastikan file serta branch sudah tampil dengan benar.

Ingat: `origin` adalah tujuan utama push, sedangkan `upstream` menyimpan referensi ke repositori sumber. Mengubah remote tidak mengubah repositori sumber.
