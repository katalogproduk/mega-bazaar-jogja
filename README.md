# Katalog EIGER Mega Bazaar Yogyakarta

Katalog customer (`index.html`) dan halaman admin (`admin.html`) untuk EIGER Mega Bazaar Yogyakarta, Kridosono Sport Hall, 24 November - 7 Desember 2026. Mekanismenya sama dengan repo `Katalog-Produk`: data diolah di browser admin lalu diterbitkan ke GitHub lewat token.

## Isi repo

| File | Isi | Diubah dari |
|---|---|---|
| `index.html` | Halaman customer | - |
| `admin.html` | Halaman admin (pakai password) | - |
| `404.html` | Supaya link seperti `/bogo` atau `/bags/backpack` bisa dibuka | - |
| `katalog.json` | Produk + stok yang tampil ke customer | Admin, tab Update katalog |
| `stok-bin.json` | Stok per bin (gudang, area jual, staging) khusus admin | Admin, ikut terbit bersama katalog |
| `promo.json` | List promo BOGO, Selected Item, Last Piece | Admin, langkah 2 |
| `master.json` | Master artikel (harga normal) | Admin, langkah 1 |
| `gambar.json` | Foto produk | Admin, langkah 3 |
| `event.json` | Nama event, lokasi, tanggal, jam, nomor WA | Admin, tab Info event |
| `banner.json` + folder `banner/` | Banner promo | Admin, tab Banner promo |

## Pemasangan (sekali saja)

1. **Repo**: buat repo publik `mega-bazaar-jogja` di organization `katalogproduk`, upload semua file di atas.
2. **GitHub Pages**: Settings → Pages → Source: *Deploy from a branch*, Branch: `main` / root. Alamat katalog: `https://katalogproduk.github.io/mega-bazaar-jogja/`.
3. **Apps Script**: tempel `Code.gs` (dikirim terpisah, **jangan di-upload ke repo** karena berisi password awal admin) ke Google Sheet baru → Extensions → Apps Script → Deploy sebagai Web app, akses *Anyone*.
4. **TRACK_URL**: salin Web app URL (berakhiran `/exec`), tempel di `index.html` pada baris `const TRACK_URL = '';`, Commit. Tanpa langkah ini halaman admin belum bisa dibuka karena login dicek ke Apps Script.
   - Login admin pertama: username `220450-Fany`. Setelah masuk, ganti password di tab **Akun**.
   - Tim mendaftar lewat tombol **Daftar** di halaman masuk admin, lalu disetujui admin di tab **Akun**. Data akun tersimpan di sheet `users` (password disimpan dalam bentuk hash).
5. **Token GitHub**: buka `admin.html`, masuk, klik *Hubungkan GitHub*, buat fine-grained token khusus repo `mega-bazaar-jogja` (Contents: Read and write).
6. **Nomor WA**: tab *Info event* → isi nomor WhatsApp → *Terbitkan info event*.

## Update harian

1. Tab *Update katalog* → pilih file `export_by_bin_DDMMYYYY_*.xlsx`.
2. Periksa tanggal stok, lokasi bazaar, dan zone yang tampil ke customer (default: Sales Area + Warehouse).
3. Klik *Buat & terbitkan katalog*. `katalog.json` dan `stok-bin.json` terbit bersamaan.

## Catatan

- `stok-bin.json` hanya ditampilkan di halaman admin, tapi repo GitHub Pages bersifat publik, jadi file ini tetap bisa diunduh orang yang tahu alamatnya.
- Data di browser (keranjang, login admin, token) memakai awalan `mb_` supaya tidak bentrok dengan katalog toko di domain `github.io` yang sama.
