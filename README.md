# korpus-daerah

Korpus peraturan daerah untuk keperluan pemeriksaan BPK (Badan Pemeriksa Keuangan): Perda (Peraturan Daerah), Perkada (Peraturan Kepala Daerah), dan SK (Surat Keputusan) Kepala Daerah. Korpus ini menjadi sumber bagi skill cari-kriteria bersama korpus-pusat.

Repositori ini hanya berisi teks peraturan publik dan metadatanya. Catatan penugasan, nama entitas yang diperiksa, data entitas, dan kredensial tidak boleh ditulis ke file, laporan, nama file, maupun pesan commit.

## Struktur

```
<provinsi>/<entitas>/<ID>.md   satu file per peraturan, dipecah per pasal
katalog.csv                    satu baris per peraturan
perubahan.csv                  peta perubahan per pasal
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
- PDF di Kotak-Masuk yang identitasnya (dibaca dari isi naskah) cocok dengan ID yang sudah ada di katalog dan file indeksnya sudah di-push langsung dipindah ke `Kotak-Masuk/duplikat/` dengan nama asli, tanpa diproses ulang dan tanpa menunggu persetujuan, berapa pun jumlah filenya. Satu-satunya pengecualian: bila korpus belum memiliki PDF maupun tautan sumber resmi untuk ID itu, salinan tersebut diproses sebagai PDF korpus (`<ID>.pdf`). Setiap pemindahan dicatat di bagian "duplikat dipindah" pada laporan.
- File yang bukan peraturan atau tidak terbaca dibiarkan di Kotak-Masuk dan dicantumkan di daftar perlu dicek.
- PDF wajib disimpan hanya untuk naskah yang tidak tersedia di sumber resmi daring.
- File di Drive tidak dihapus.

## Konvensi penamaan

- Folder provinsi: singkatan baku tanpa awalan (`kalbar`).
- Folder entitas: awalan `prov-`, `kab-`, atau `kota-`. Huruf kecil, tanda hubung.
- ID peraturan sekaligus menjadi nama file: `<ID>.md` di repositori, `<ID>.pdf` di Google Drive.
- Dokumen pendukung (buku manual, petunjuk teknis, atau pedoman terbitan instansi yang bukan naskah peraturan, tetapi dinyatakan sebagai lampiran atau dirujuk oleh peraturan induknya) disimpan di folder yang sama dengan peraturan induknya dengan nama `<ID-induk>_<KETERANGAN>.pdf`; `<KETERANGAN>` huruf kapital dengan tanda hubung, misalnya `PERBUP_KAB-LANDAK_15_2025_JUKNIS.pdf`. Dokumen pendukung tidak mendapat ID, file indeks, atau baris katalog sendiri, dan tidak dicatat di kolom `tautan_pdf_drive`; judul, dasar keterkaitannya, dan tautan Drive-nya ditulis di bawah heading `## Lampiran` pada file indeks peraturan induk. Dokumen terbitan instansi yang tidak punya peraturan induk tidak disimpan di korpus.
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

## perubahan.csv

Peta perubahan per pasal. Peta ini tidak menyalin bunyi pasal; bunyi yang berlaku dikutip langsung dari naskah pengubah yang ditunjuk. Versi konsolidasi tidak disusun.

Satu baris mewakili satu unsur naskah induk yang terkena oleh satu naskah pengubah. Kolom, berurutan:

| Kolom | Isi |
|---|---|
| id_induk | ID peraturan yang teksnya berubah |
| unsur | `pasal`, `bab`, `bagian`, `paragraf`, `judul-bagian`, `penjelasan`, `lampiran`, atau `naskah` (seluruh naskah) |
| rujukan | Alamat unsur di naskah induk, misalnya `12`, `9A`, `BAB VIII Bagian Keenam`, `Lampiran II` |
| jenis_perubahan | `diubah`, `disisipkan`, `dihapus`, `dicabut`, `tidak-mengikat-mk`, atau `ditetapkan-menjadi-uu` |
| id_pengubah | ID peraturan pengubah atau pencabut; untuk putusan Mahkamah Konstitusi (MK): `PUTUSANMK_<nomor>-PUU-<kode tahun register>_<tahun register>`, misalnya `PUTUSANMK_91-PUU-XVIII_2020` untuk perkara 91/PUU-XVIII/2020 |
| lokasi | Letak perintah perubahan di naskah pengubah, ditulis persis, misalnya `Pasal I angka 5` atau `Pasal 176 angka 3`; untuk putusan MK: `Amar angka <n>` |
| rincian | Kalimat perintah perubahan disalin dari naskah pengubah sampai sebelum kata "sehingga"; untuk putusan MK: bunyi amar yang menyangkut pasal itu |
| berlaku_sejak | Tanggal mulai berlaku perubahan menurut ketentuan penutup atau peralihan naskah pengubah; untuk putusan MK: tanggal putusan diucapkan; `AAAA-BB-HH` |
| status_review | `lolos-otomatis`, `perlu-dicek`, atau `terverifikasi` |
| catatan_cek | Alasan singkat bila `perlu-dicek` |

Aturan pengisian:

1. Satuan baris adalah pasal. Ayat, huruf, atau angka yang terkena dicatat di `rincian`, karena naskah pengubah menulis ulang pasal itu secara utuh ("sehingga Pasal N berbunyi sebagai berikut").
2. `diubah`: isi pasal berubah, termasuk ayat atau huruf yang disisipkan, ditambahkan, atau dihapus di dalamnya. `disisipkan`: pasal atau unsur baru. `dihapus`: pasal dihapus lewat perintah perubahan. `dicabut`: pasal dicabut atau dinyatakan tidak berlaku lewat ketentuan penutup peraturan lain. `tidak-mengikat-mk`: pasal, ayat, atau frasa dinyatakan bertentangan dengan UUD 1945 dan tidak mempunyai kekuatan hukum mengikat oleh putusan MK. Bila yang terkena hanya sebagian pasal (ayat, huruf, atau frasa), bagian itu disebut di `rincian`.
3. `id_induk` adalah naskah yang teksnya benar-benar berubah. Pasal sisipan tetap memakai `id_induk` peraturan asal, sehingga riwayatnya terbaca dengan mengurutkan baris per `id_induk` dan `rujukan` berdasarkan `berlaku_sejak`.
4. Naskah perubahan yang disebut dalam frasa "sebagaimana telah diubah dengan" tidak ikut diubah. Perubahan berikutnya tercatat pada `id_induk` asal, bukan pada naskah perubahan sebelumnya. Aturan yang sama berlaku untuk kolom `diubah_dicabut_oleh` di katalog: naskah perubahan berstatus `diubah` hanya bila norma miliknya sendiri diubah.
5. Isi diambil dari bunyi naskah pengubah yang dibaca, bukan dari judul atau ringkasan situs. Untuk putusan MK, isi diambil dari amar putusan yang dibaca (Pasal.id atau situs MK); putusan MK tidak diindeks dan tidak dicatat di katalog.
6. Perppu (Peraturan Pemerintah Pengganti Undang-Undang) yang ditetapkan menjadi UU: penetapan tidak mengubah isi, jadi status Perppu di katalog tetap `berlaku` dan UU penetapan tidak dicatat di `diubah_dicabut_oleh`. Hubungannya dicatat satu baris: `unsur` = `naskah`, `rujukan` = `seluruh`, `jenis_perubahan` = `ditetapkan-menjadi-uu`, `id_pengubah` = UU penetapan, `lokasi` = pasal penetapan. Perppu yang ditolak DPR berstatus `dicabut`. Perubahan yang dibuat Perppu atas peraturan lain memakai ID Perppu sebagai `id_pengubah`, karena teksnya ada di naskah Perppu. Bila naskah Perppu tidak diindeks terpisah dan teksnya hanya ada sebagai lampiran UU penetapan, ID UU penetapan yang dipakai. Saat dikutip: "Pasal N Perppu X yang telah ditetapkan menjadi Undang-Undang dengan UU Y".
7. Baris diberi `perlu-dicek` bila naskah pengubahnya berstatus `perlu-dicek` di katalog atau bila tanggal berlakunya tidak terbaca; alasannya ditulis di `catatan_cek`.

Cara membaca rantai perubahan:

- Ambil semua baris dengan `id_induk` dan `rujukan` yang dicari, lalu urutkan berdasarkan `berlaku_sejak`. Bunyi yang berlaku pada suatu tanggal adalah bunyi pada baris terakhir yang `berlaku_sejak`-nya tidak melewati tanggal itu. Bila tidak ada baris sebelum tanggal itu, pakai bunyi naskah induk.
- Setiap kali mengutip pasal dari peta, baca juga ketentuan peralihan dan penutup setiap naskah pengubah dalam rantai (biasanya Pasal II), karena di sana dapat diatur penundaan, batas waktu, atau masa transisi untuk pasal tertentu.
- Baca `rincian` setiap baris: bila yang terkena hanya sebagian pasal, bagian lain pasal itu tetap mengikuti bunyi sebelumnya.
- Peta lengkap untuk suatu induk hanya bila setiap ID di `diubah_dicabut_oleh` pada katalog punya paling sedikit satu baris di perubahan.csv (putusan MK tidak tercatat di katalog, jadi tidak ikut pemeriksaan ini). Bila belum lengkap, misalnya karena naskah pengubah belum ada di korpus, sampaikan peringatan sebelum mengutip bunyi pasal induk.

## Format file indeks

Sama dengan korpus-pusat (lihat README korpus-pusat): front matter `id`, `jenis`, `nomor`, `tahun`, `judul`, `sumber_teks`; heading Pembukaan, BAB, `### Pasal N`, Penutup, Penjelasan (dengan Penjelasan Umum), dan Lampiran. SK yang tidak berpasal memakai heading sesuai diktum (KESATU, KEDUA).

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
