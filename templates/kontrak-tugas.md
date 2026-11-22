# Template: Kontrak Tugas

Salin file ini, ganti namanya sesuai tugas, lalu isi semua kolom.
Kolom yang kosong berarti kontrak belum boleh dikirim ke sub-agent.
Acuan: bagian "Kontrak tugas" di `../PROTOCOL.md`.

---

**Nomor / nama tugas:** _(isi: mis. T-001 — judul singkat tugas)_

## Tugas (kata-kata user)

> _(Tulis persis perintah user, tanpa ditambah atau dikurangi. Satu tugas =
> satu hasil konkret yang diminta.)_

## Konteks

_(Fakta yang sudah diketahui dan relevan dengan tugas ini saja — bukan
seluruh riwayat percakapan. Sertakan sumbernya bila ada.)_

-
-

## Batasan

_(Apa yang tidak boleh dilakukan selama tugas ini berjalan.)_

- Biaya: _(isi: mis. Rp0 — tidak ada pembelian / langganan / biaya apa pun)_
- Akun & kredensial: tidak menerima, tidak menyimpan, tidak menuliskan
  kredensial apa pun di file, log, atau pesan antar-agent
- Pihak luar: _(isi: mis. tidak ada posting / kirim / submit keluar tanpa
  gerbang persetujuan di bawah)_
- Lingkup: _(isi: hal-hal di luar tugas yang tidak ikut dikerjakan)_

## Peran yang ditugaskan

| Peran | Ditugaskan ke | Lingkup bagiannya |
|---|---|---|
| Riset | _(nama sesi sub-agent)_ | _(isi: fakta apa yang harus dikumpulkan)_ |
| Builder | _(nama sesi sub-agent)_ | _(isi: apa yang harus dibangun)_ |
| Checker | _(nama sesi sub-agent — wajib sesi berbeda dari Builder)_ | _(isi: apa yang harus diperiksa)_ |

## Format hasil

- Bentuk: _(isi: file / ringkasan / daftar / artefak lain)_
- Disimpan di: _(isi: path file atau tautan tempat hasil akhir berada)_
- Serah-terima memakai template `serah-terima.md`

## Kriteria selesai

_(Bukti yang membuat tugas ini dianggap beres. Tulis yang bisa dicek,
bukan kesan umum.)_

- [ ] _(isi: mis. file hasil ada di path yang ditentukan dan bisa dibuka)_
- [ ] _(isi: mis. angka / tanggal / tautan cocok dengan sumbernya)_
- [ ] _(isi: mis. laporan checker berputusan Lolos atau Lolos dengan catatan)_

## Gerbang persetujuan terkait

_(Centang gerbang yang mungkin dilewati tugas ini. Setiap gerbang yang
tercentang wajib berhenti dan menunggu persetujuan user dulu.)_

- [ ] Login ke akun apa pun — user mengetik kredensialnya sendiri
- [ ] Posting / kirim pesan ke pihak luar atas nama user
- [ ] Transfer uang / wallet, pembayaran, pembelian
- [ ] Menghapus data secara permanen
- [ ] Tidak ada gerbang pada tugas ini
