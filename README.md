# WebAR Buku Interaktif — Starter MindAR

Paket siap deploy untuk coba *image tracking* WebAR gratis. Tampilan objek demo: planet bercincin dalam format GLB yang dibuat khusus untuk contoh proyek ini.

## Yang ada di ZIP ini

- `index.html` — website kamera AR, memakai gambar target demo resmi MindAR.
- `target-demo.html` — halaman gambar yang harus ditampilkan di laptop/dicetak saat mengetes.
- `assets/planet.glb` — model 3D demo (digunakan lokal, tanpa sumber objek eksternal).

## Cara cepat mencoba (GitHub Pages)

1. Buka https://github.com/ dan login.
2. Create repository baru, misal `buku-ar`. Atur **Public**.
3. Upload file `index.html`, `target-demo.html`, dan folder `assets/` (pertahankan struktur). Commit.
4. Buka **Settings → Pages**. Pada **Build and deployment** pilih **Deploy from a branch**, branch `main`, folder `/(root)` lalu Save.
5. Setelah website terbit, buka `https://USERNAME.github.io/buku-ar/` di HP.
6. Izinkan akses kamera.
7. Di LAPTOP, buka `https://USERNAME.github.io/buku-ar/target-demo.html`, tampilkan gambar demo di layar. Arahkan kamera HP ke gambar tersebut.
8. Planet 3D seharusnya muncul di atas gambar; bila tidak, cek koneksi Internet, kamera, cahaya, dan status permisi.

> Kamera dari HP biasa memerlukan HTTPS. Jangan hanya membuka `index.html` langsung sebagai file. Selain itu, URL `http://192.168...` dari laptop biasanya tidak memenuhi syarat secure context browser HP.

## Menukar gambar demo menjadi gambar dari buku Heyzine

1. Simpan gambar yang persis muncul di halaman buku dalam bentuk PNG/JPG, misalnya `gambar-halaman-5.png`.
2. Buka compiler resmi: https://hiukim.github.io/mind-ar-js-doc/tools/compile/
3. Upload gambar → **Start** → tunggu selesai → **Download** file `.mind`.
4. Rename file hasilnya menjadi `targets.mind`. Tempatkan di folder yang sama dengan `index.html`.
5. Di `index.html`, cari: 
   `imageTargetSrc: https://cdn.jsdelivr.net/gh/hiukim/mind-ar-js@1.2.5/examples/image-tracking/assets/card-example/card.mind;`
6. Ganti menjadi: 
   `imageTargetSrc: ./targets.mind;`
7. Upload/commit perubahan `index.html` dan `targets.mind` ke GitHub. Setelah Pages update, scan gambar buku menggunakan HP.
8. Pastikan gambar di layar atau cetakan memiliki detail, tekstur, kontras dan tidak terpantul cahaya. Target sebaiknya bukan area kosong / sekadar logo kecil.

## Menukar model 3D

1. Siapkan `model.glb` sendiri (pastikan memang boleh dipakai). Bila model cuma ada di Assemblr dan tidak bisa diekspor, cari/buat ulang model 3D lain; link QR Assemblr yang sudah mati tidak mengandung modelnya.
2. Letakkan di folder `assets/`.
3. Di `index.html` ubah `src="./assets/planet.glb"` menjadi `src="./assets/model.glb"`.
4. Sesuaikan nilai `scale` (`0.78 0.78 0.78`) dan `position` (`0 0 0.22`) sesuai ukuran/pusat model. Nilai itu relatif terhadap lebar gambar target, bukan sentimeter.
5. Commit lagi ke GitHub.

## Menghubungkan ke Heyzine

1. Buka editor Heyzine untuk buku yang lu punya hak edit.
2. Masuk halaman yang ingin diberi AR (mis. halaman 5).
3. Interactions → Link, gambar area yang akan menjadi tombol "Lihat AR".
4. Pilih **Open Link** (web URL); isi URL GitHub Pages. Usahakan buka di tab baru/top-level browser supaya permintaan kamera tidak terhalang iframe.
5. Simpan perubahan. Uji dari HP.

Catatan: di HP yang sama, kamera tidak bisa memindai layar buku yang sedang terbuka di HP itu sendiri. Gunakan buku cetak/laptop/HP lain sebagai tempat gambar target. Jika pengguna butuh 3D dalam halaman digital pada HP yang sama, itu pengalaman 3D viewer, bukan MindAR image tracking yang memindai gambar fisik.

## Troubleshooting

- **Kamera hitam/tidak muncul**: buka situs langsung dari HTTPS di Safari/Chrome, bukan dalam browser mini aplikasi atau iframe; cek izin kamera dan browser mendukung WebGL.
- **Objek tak terlihat**: pastikan gambar cocok dengan `.mind`; kualitas gambar jelas; pencahayaan merata; koneksi Internet aktif; cek apakah model GLB dapat dimuat.
- **Objek terlalu besar/kecil atau terbalik**: ubah scale/position/rotation di tag `a-gltf-model`.
- **404**: cek ejaan nama file dan huruf besar-kecil di GitHub; `targets.mind` harus diletakkan di lokasi yang tepat.
- **Link QR lama Assemblr tidak aktif**: ini adalah proyek WebAR baru dengan URL dan QR baru; tidak otomatis memulihkan link QR lama.

Dokumentasi: https://hiukim.github.io/mind-ar-js-doc/ | https://docs.github.com/en/pages | https://heyzine.com/faq
