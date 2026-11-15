# korpus-daerah

Korpus peraturan daerah untuk keperluan pemeriksaan BPK (Badan Pemeriksa Keuangan): Perda (Peraturan Daerah), Perkada (Peraturan Kepala Daerah), dan SK (Surat Keputusan) Kepala Daerah. Korpus ini menjadi sumber bagi skill cari-kriteria bersama korpus-pusat.

Repositori ini hanya berisi teks peraturan publik dan metadatanya. Catatan penugasan, nama entitas yang diperiksa, data entitas, dan kredensial tidak boleh ditulis ke file, laporan, nama file, maupun pesan commit.

## Struktur

```
<provinsi>/<entitas>/<ID>.md   satu file per peraturan, dipecah per pasal
katalog.csv                    satu baris per peraturan
laporan/AAAA-BB.md             laporan berkala
```

- Pemerintah provinsi adalah entitas sejajar dengan kabupaten/kota. Contoh: `kalbar/prov-kalbar/`, `kalbar/kab-landak/`, `kalbar/kota-singkawang/`.
- Tingkat pemda saja; tidak ada folder per unit kerja.
- Folder provinsi dan entitas dibuat saat naskah pertamanya masuk.
- Tag isu memakai `tag.csv` di korpus-pusat.

## Google Drive

Naskah PDF disimpan di Google Drive akun khusus, di bawah folder induk `Peraturan/`:

```
Peraturan/
├── Kotak-Masuk/              PDF yang belum diproses, nama file bebas (pusat maupun daerah)
│   └── duplikat/             PDF duplikat dari Kotak-Masuk; tidak dipindai, dikosongkan pemilik korpus secara berkala
├── Korpus-Pusat/naskah/<jenis>/<ID>.pdf
└── Korpus-Daerah/<provinsi>/<entitas>/<ID>.pdf
```

- Kotak-Masuk bukan bagian korpus dan tidak dicatat di katalog. Identitas naskah dibaca dari isi PDF, bukan dari nama file.
- PDF yang sudah terindeks dipindah dari Kotak-Masuk ke folder korpusnya dengan nama `<ID>.pdf`.
- PDF di Kotak-Masuk yang ID-nya sudah ada di katalog dipindah ke `Kotak-Masuk/duplikat/` dengan nama asli, bila korpus sudah memiliki PDF atau tautan sumber resmi. Bila salinan itu satu-satunya PDF, ia diproses sebagai PDF korpus. Bila versinya berbeda atau mutunya lebih baik dari yang terindeks, ia dibiarkan di Kotak-Masuk dan dicantumkan di daftar perlu dicek.
- File yang bukan peraturan atau tidak terbaca dibiarkan di Kotak-Masuk dan dicantumkan di daftar perlu dicek.
- PDF wajib disimpan hanya untuk naskah yang tidak tersedia di sumber resmi daring.
- File di Drive tidak dihapus.

## Konvensi penamaan

- Folder provinsi: singkatan baku tanpa awalan (`kalbar`).
- Folder entitas: awalan `prov-`, `kab-`, atau `kota-`. Huruf kecil, tanda hubung.
- ID peraturan sekaligus menjadi nama file: `<ID>.md` di repositori, `<ID>.pdf` di Google Drive.
- ID ditulis huruf kapital dengan garis bawah sebagai pemisah: `<JENIS>_<ENTITAS>_<NOMOR>_<TAHUN>`. Contoh: `PERBUP_KAB-LANDAK_15_2025`.
- Lampiran yang disimpan sebagai PDF terpisah diberi nama `<ID>_LAMPIRAN-I.pdf`, `<ID>_LAMPIRAN-II.pdf`, dan seterusnya, di folder yang sama dengan PDF induknya. Lampiran tunggal: `<ID>_LAMPIRAN.pdf`.
- Tanggal ditulis `AAAA-BB-HH`.

## katalog.csv

Kolom, berurutan:

| Kolom | Isi |
|---|---|
| id | ID peraturan sesuai konvensi |
| jenis | Jenis peraturan |
| nomor | Nomor peraturan |
| tahun | Tahun peraturan |
| judul | Judul lengkap |
| penerbit | Pemda penetap |
| status | `berlaku`, `diubah`, atau `dicabut` |
| berlaku_sejak | Tanggal mulai berlaku menurut ketentuan penutup naskah |
| berlaku_sampai | Tanggal mulai berlakunya peraturan pencabut; kosong bila masih berlaku |
| diubah_dicabut_oleh | ID peraturan pengubah atau pencabut; beberapa ID dipisah titik koma; "tidak ditemukan pengganti di korpus" bila tidak ada |
| tautan_sumber | Tautan resmi (JDIH, Jaringan Dokumentasi dan Informasi Hukum, pemda); kosong bila tidak ditemukan |
| tautan_pdf_drive | Tautan PDF di Google Drive, bila disimpan; bila lampiran disimpan terpisah, tautan induk lalu tautan lampiran, dipisah titik koma |
| tag_isu | Tag dari tag.csv korpus-pusat, dipisah titik koma |
| tag_jenis_pemeriksaan | `keuangan`, `kinerja`, `pdtt` (Pemeriksaan Dengan Tujuan Tertentu); boleh lebih dari satu |
| tanggal_verifikasi | Tanggal terakhir status dicek ke sumber luar |
| status_review | `lolos-otomatis`, `perlu-dicek`, atau `terverifikasi` |
| catatan_cek | Alasan singkat bila `perlu-dicek` |
| provinsi | Folder provinsi |
| dasar_hukum | ID peraturan di korpus-pusat yang menjadi dasar (bagian Mengingat atau pasal yang mendelegasikan); dipisah titik koma |
| dasar_status | Status peraturan dasar menurut katalog korpus-pusat pada tanggal_cek |
| tanggal_cek | Tanggal dasar_status dicek |

Nilai yang mengandung koma diapit tanda kutip ganda. Urutan dan nama kolom tidak diubah tanpa persetujuan pemilik korpus.

Peraturan yang dicabut tidak dihapus. Masa berlakunya dicatat di katalog karena kriteria dipilih berdasarkan periode yang diperiksa.

Status peraturan daerah disimpulkan dari ketentuan penutup peraturan pengganti yang ada di korpus, lalu dicek ke JDIH pemda bila dapat diakses. Akurasinya bergantung pada kelengkapan korpus pemda yang bersangkutan.

## Format file indeks

Sama dengan korpus-pusat (lihat README korpus-pusat): front matter `id`, `jenis`, `nomor`, `tahun`, `judul`, `sumber_teks`; heading Pembukaan, BAB, `### Pasal N`, Penjelasan, dan Lampiran. SK yang tidak berpasal memakai heading sesuai diktum (KESATU, KEDUA).

## Pemeriksaan otomatis dan status_review

Sama dengan korpus-pusat: enam pemeriksaan (identitas, naskah final, mutu OCR, urutan pasal, duplikat, masa berlaku). Semua lulus: `lolos-otomatis`. Ada yang gagal: `perlu-dicek` dengan alasannya. `terverifikasi` hanya setelah teks pasal dicocokkan dengan PDF.

## Laporan

`laporan/AAAA-BB.md` berisi enam bagian tetap: naskah masuk, perubahan status, perlu dicek, usulan tag baru, kendala akses, dan duplikat dipindah. Laporan korpus-daerah terpisah dari laporan korpus-pusat. Laporan bulan yang sama diperbarui dengan menambah, bukan menimpa.

## Pesan commit

```
tambah: <ID> - <judul singkat> [<status_review>]
status: <ID> <status lama> -> <status baru> oleh <ID pengubah>
katalog: <perubahan metadata dan alasannya>
laporan: AAAA-BB
skema: <perubahan yang disetujui>
```
