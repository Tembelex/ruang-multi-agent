# Template: Laporan Checker

Diisi sub-agent Checker untuk koordinator. Checker wajib sesi yang
berbeda dari Builder yang menghasilkan objek pemeriksaan.
Acuan: `../agents/checker.md` dan bagian "Kriteria selesai" pada kontrak.

---

**Tanggal pemeriksaan:** _(isi: tanggal, dan jam + zona waktu bila relevan)_
**Pemeriksa:** _(isi: nama sesi Checker)_

## Objek yang diperiksa

- Hasil: _(isi: path file / tautan persis seperti pada serah-terima Builder)_
- Dibangun oleh: _(isi: nama sesi Builder)_
- Serah-terima acuan: _(isi: tautan / path dokumen serah-terimanya)_

## Kontrak acuan

- Nomor / nama tugas: _(isi sesuai kontrak tugas)_
- Kriteria selesai pada kontrak:
  - _(salin kriteria satu per satu; tiap kriteria dinilai pada bagian Temuan)_

## Putusan

_(Lingkari / tebalkan satu. Hapus dua lainnya.)_

**Lolos** / **Lolos dengan catatan** / **Ditolak**

Alasan ringkas putusan: _(isi: 1–2 kalimat)_

## Temuan (urut dampak)

_(Urutkan dari yang paling berpengaruh ke hasil akhir sampai yang paling
kecil. Satu temuan per baris: apa masalahnya, di mana letaknya, dan
buktinya.)_

| # | Temuan | Letak | Bukti / cara cek | Dampak |
|---|---|---|---|---|
| 1 | _(isi)_ | _(isi: bagian / baris / file)_ | _(isi)_ | _(isi: Tinggi / Sedang / Rendah)_ |
| 2 | _(isi)_ | _(isi)_ | _(isi)_ | _(isi)_ |
| 3 | _(isi)_ | _(isi)_ | _(isi)_ | _(isi)_ |

Hal yang sudah diperiksa dan ternyata benar (agar tidak dicek ulang):

-
-

## Perbaikan yang diminta

_(Wajib diisi spesifik untuk putusan Ditolak; untuk Lolos dengan catatan,
isi catatan yang perlu ditindaklanjuti. Perbaikan ditulis sebagai tindakan
konkret, bukan penilaian umum.)_

- [ ] _(isi: perbaikan 1 — apa yang diubah, di mana, menjadi seperti apa)_
- [ ] _(isi: perbaikan 2)_
- Setelah perbaikan: _(isi: siapa yang memeriksa ulang — Checker yang sama
  atau sesi Checker baru)_
