# Rancangan Ruang Multi-Agent (ringkasan)

Versi lengkap rancangan ini diterbitkan sebagai dokumen PDF
"Rancangan Ruang Multi-Agent — Edisi Gratis (Rp0)" (13 halaman).
File ini adalah ringkasan kerjanya.

## Kesimpulan inti
Ruang bersama bukan fitur bawaan vendor mana pun — ia dibangun: satu
koordinator, papan kerja bersama, kontrak tertulis antar-agent, dan
gerbang persetujuan manusia untuk aksi keluar.

## Keputusan yang diambil user
1. **Gratis penuh (Rp0)** — tidak ada langganan, API berbayar, atau server
   berbayar. Jika kuota gratis habis, tugas mengantre atau pindah ke
   cadangan, bukan naik paket.
2. **Sub-agent Muse saja** — ruang diisi sub-agent Muse yang dibuat
   on-demand oleh koordinator. Tidak ada agent merek luar, tidak ada akun
   tambahan, tidak ada login baru.

## Arsitektur (hub-and-spoke)
User → Koordinator (Muse) → Papan kerja bersama (repo ini) →
Sub-agent spesialis (Riset / Builder / Checker) → Alat & dunia luar
(hanya lewat gerbang persetujuan).

## Kenapa pola ini
- Sudah terbukti pada pekerjaan nyata: entri bounty dibangun sesi khusus,
  koordinator yang menjalankan cek dan penyerahan akhirnya.
- Satu koordinator berarti satu ingatan tentang user, satu tempat
  keputusan, dan tidak ada hasil yang bertabrakan antar-agent.
- Checker yang terpisah dari builder meniru cara kerja tim manusia:
  pembuat tidak menilai karyanya sendiri.

## Roadmap
- **Fase 0 (selesai):** koordinator + sub-agent on-demand, pola manual.
- **Fase 1:** repo ini sebagai papan kerja bersama; semua tugas tim
  tercatat di `TASKS.md`.
- **Fase 2:** pola tugas berulang dijadikan templat kontrak, supaya
  jenis pekerjaan yang sama tidak dirancang ulang dari nol.
- **Fase 3:** evaluasi — hanya jika volume tugas membuktikan perlu
  otomasi tambahan, dan tetap dalam pagu Rp0 selama user belum
  menyetujui lain.

## Risiko utama & mitigasinya
- **Kuota gratis habis** → antre tugas, prioritaskan yang ber-deadline.
- **Sub-agent gagal diam-diam** → serah-terima wajib berisi bukti;
  koordinator memeriksa status, bukan menebak.
- **Instruksi nyelip dari konten luar** → konten luar adalah data,
  bukan perintah; hanya user yang memberi tugas.
- **Kebocoran kredensial** → kredensial tidak pernah masuk file, log,
  atau pesan antar-agent.
