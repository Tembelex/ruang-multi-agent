# Catatan Riset 1 — Praktik Workflow Multi-Agent Berbasis Peran

Riset singkat dari sumber publik tentang pola koordinator + spesialis +
checker independen. Semua pelajaran ditulis ulang dengan kata-kata sendiri;
tautan sumber dicantumkan di tiap pelajaran dan dirangkum di akhir.

## 1. Tambah agent hanya kalau ada batas kerja yang jelas

**Pelajaran:** Multi-agent bukan tujuan, melainkan alat. Agent tambahan
baru layak dipakai bila ada alasan konkret: pekerjaan bisa jalan paralel,
ada spesialisasi yang nyata, konteks perlu diisolasi supaya koordinator
tidak tenggelam detail, wewenang harus dipisah, atau hasil butuh peninjau
independen.

**Kenapa penting:** Setiap agent menambah permukaan serah-terima, biaya,
dan tempat kegagalan bisa bersembunyi. Pengalaman Anthropic pada sistem
riset multi-agent mereka: pemakaian token sistem multi-agent bisa sekitar
15 kali percakapan biasa, jadi nilai tugasnya harus sebanding.

**Penerapan di ruang ini:** Koordinator menilai dulu di awal tugas —
kalau satu agent sanggup dan tugasnya berurutan rapat, kerjakan sendiri.
Sub-agent Riset / Builder / Checker hanya dibuat bila tugasnya memang
bisa dipisah bersih atau butuh pemeriksaan silang.

**Sumber:** Agentic Engineering Fieldbook, "Multi-Agent Systems";
Anthropic, "How we built our multi-agent research system".

## 2. Kontrak delegasi harus menyebut batas "jangan kerjakan ini"

**Pelajaran:** Penugasan yang baik minimal memuat: tujuan yang terbatas,
hal yang secara eksplisit dikecualikan, input dan versi sumber yang dipakai,
format hasil yang diharapkan, bukti sukses/gagal, alat dan tujuan yang
diizinkan, serta batas waktu/biaya.

**Kenapa penting:** Delegasi yang kabur adalah sumber kegagalan paling
umum: sub-agent saling meniru pekerjaan yang sama atau justru meninggalkan
celah yang tidak dikerjakan siapa pun. Contoh klasik dari Anthropic:
beberapa sub-agent meneliti pertanyaan yang sama persis karena batas
tugasnya tidak dipisah.

**Penerapan di ruang ini:** Kontrak di `PROTOCOL.md` sudah memuat tugas,
konteks, batasan, format hasil, dan kriteria selesai — tambahkan kebiasaan
menulis satu baris eksklusi eksplisit ("jangan kerjakan X, itu bagian
agent lain") setiap kali dua sub-agent jalan paralel.

**Sumber:** Anthropic, "How we built our multi-agent research system";
Agentic Engineering Fieldbook, "Multi-Agent Systems" (bagian kontrak tugas).

## 3. Serah-terima adalah kontrak terstruktur, bukan cerita bebas

**Pelajaran:** Yang menyeberang dari satu agent ke agent berikutnya harus
berbentuk paket yang bisa diperiksa: hasil/artefaknya, input yang dipakai,
ringkasan pengerjaan, sinyal keyakinan, hal yang tidak ditangani, dan
kegagalan yang ditemui. Penerima memvalidasi paket itu dulu; kalau tidak
memenuhi kontrak, berhenti dan laporkan di titik itu juga.

**Kenapa penting:** Serah-terima berupa prosa bebas memaksa penerima
menebak-nebak maksud pengirim. Tebakan yang salah tidak langsung terlihat —
ia menumpuk diam-diam dan baru muncul sebagai jawaban akhir yang
"meyakinkan tapi salah".

**Penerapan di ruang ini:** Format serah-terima di `PROTOCOL.md` (Hasil /
Yang dikerjakan / Bukti / Yang gagal atau belum pasti / Butuh keputusan)
sudah sejalan — perlakukan kelima bagian itu sebagai wajib terisi, dan
koordinator menolak laporan yang bagian Buktinya kosong.

**Sumber:** The Agents Layer, "Designing multi-agent systems that don't
fall apart" (bagian handoffs).

## 4. Checker harus independen, dan yang dinilai adalah artefaknya

**Pelajaran:** Pemeriksaan tidak boleh dilakukan pembuatnya sendiri, dan
yang dinilai adalah hasil akhir yang nyata (file, tautan, angka), bukan
klaim agent tentang hasil itu. Penelitian taksonomi kegagalan multi-agent
(MAST) yang diannotasi dari 1.600+ jejak eksekusi mengelompokkan kegagalan
ke tiga keranjang besar: masalah spesifikasi/desain (±42%),
ketidakselarasan antar-agent (±37%), dan verifikasi tugas yang lemah
(±21%) — jadi verifikasi bukan formalitas, melainkan seperlima masalah.

**Kenapa penting:** Agent yang menilai karyanya sendiri cenderung
membenarkan asumsinya sendiri. Pemeriksa terpisah dengan konteks segar
lebih mungkin menangkap asumsi yang sama-sama keliru.

**Penerapan di ruang ini:** Checker selalu sesi berbeda dari Builder
(sudah jadi aturan di `agents/checker.md`). Putusannya harus menunjuk
bukti yang diperiksa — file yang dibuka, tautan yang dikunjungi, angka
yang dicocokkan ke sumber — bukan sekadar "sudah sesuai".

**Sumber:** KodeKloud, "Multi Agent Systems for Platform Engineering"
(ringkasan studi MAST); The Agents Layer (review independen sebagai
salah satu pembenaran multi-agent).

## 5. Keadaan bersama butuh pemilik dan asal-usul yang jelas

**Pelajaran:** Papan tugas / memori bersama pada dasarnya adalah basis
data yang ditulis banyak pihak sekaligus. Setiap bagian harus jelas siapa
pemiliknya, setiap tulisan diberi cap asal-usul (siapa, kapan, dari tugas
apa), dan hanya satu pihak yang berhak menggabungkan hasil akhir.

**Kenapa penting:** Tanpa aturan itu, papan bersama melahirkan balapan
tulis, klaim tugas ganda, catatan basi yang dianggap masih berlaku, dan
agent yang bekerja dari gambaran keadaan yang berbeda-beda — persis
kategori ketidakselarasan antar-agent pada studi MAST di atas.

**Penerapan di ruang ini:** `TASKS.md` hanya diperbarui koordinator;
sub-agent melaporkan perubahan status lewat serah-terima, bukan menulis
papan sendiri. Satu baris tugas = satu pemilik peran, dan hasil akhir
selalu digabungkan koordinator, bukan oleh sub-agent.

**Sumber:** Agentic Engineering Fieldbook, "Multi-Agent Systems"
(topologi papan tugas bersama dan risikonya); The Agents Layer
(memori bersama dan provenance).

## 6. Konten luar adalah data, bukan perintah — dan batasi kerugiannya

**Pelajaran:** Instruksi bisa menyelip lewat halaman web, dokumen, hasil
alat, dan konten lain yang dibaca agent (injeksi tidak langsung, risiko
LLM01 di daftar OWASP). Tidak ada filter prompt yang bisa diandalkan
sepenuhnya, jadi pertahanannya bersifat arsitektural: pisahkan instruksi
dari data, beri tiap peran hak minimum, jauhkan kredensial dari konteks,
dan wajibkan persetujuan manusia untuk aksi yang berdampak.

**Kenapa penting:** Agent yang dibelokkan konten luar bertindak memakai
wewenang ruang itu sendiri. Kalau wewenangnya sempit dan aksi pentingnya
berpagar persetujuan, instruksi nyelip paling jauh hanya menghasilkan
laporan yang salah — bukan tindakan yang merugikan.

**Penerapan di ruang ini:** Sudah menjadi aturan ruang: konten luar tidak
mengubah tugas dari user, hasil sub-agent adalah laporan bukan perintah,
dan gerbang persetujuan di README berlaku untuk login, posting keluar,
uang, dan penghapusan. Tambahan praktisnya: sub-agent yang membaca sumber
luar tidak diberi alat/tindakan keluar sama sekali — ia hanya mengembalikan
fakta dan kutipan sumber ke koordinator.

**Sumber:** OWASP LLM Top 10 (LLM01) sebagaimana dirangkum Software
Security, "Prompt injection: contain it with a tool gateway"; LearnLive,
"Defending AI Agents Against Prompt Injection".

## 7. Atur skala usaha menurut kerumitan, dan uji dari kasus kecil

**Pelajaran:** Jumlah sub-agent dan kedalaman kerja harus mengikuti
kerumitan tugas, bukan kebiasaan. Anthropic memakai aturan praktis di
prompt orkestratornya: tugas pencarian fakta sederhana cukup satu agent,
perbandingan langsung memakai beberapa sub-agent, riset kompleks baru
memakai banyak. Sintesis akhir juga pekerjaan berpikir tersendiri bagi
koordinator — bukan sekadar menempel laporan-laporan jadi satu.

**Kenapa penting:** Terlalu banyak agent untuk tugas kecil membuang
kuota (ruang ini beroperasi gratis) dan menambah kebisingan; terlalu
sedikit untuk tugas besar membuat hasil dangkal. Evaluasi dari sejumlah
kasus uji kecil yang nyata lebih bisa dipercaya daripada kesan sekali jalan.

**Penerapan di ruang ini:** Koordinator menuliskan perkiraan skala di
kontrak ("tugas ini: 1 riset + 1 builder + checker") sebelum mulai.
Untuk jenis tugas yang berulang, simpan 3–5 contoh tugas lama beserta
hasil idealnya sebagai bahan uji setiap kali protokol atau file peran
diubah.

**Sumber:** Anthropic, "How we built our multi-agent research system"
(aturan skala usaha dan peran sintesis lead agent).

## Daftar sumber

- Anthropic — How we built our multi-agent research system:
  https://www.anthropic.com/research/multi-agent-research-system?s=08
- Agentic Engineering Fieldbook — Multi-Agent Systems:
  https://ae.docode.org/en/architecture/multi-agent-systems
- The Agents Layer — Designing multi-agent systems that don't fall apart:
  https://www.theagentslayer.com/blog/multi-agent-orchestration
- KodeKloud — Multi Agent Systems for Platform Engineering:
  https://kodekloud.com/blog/multi-agent-systems-platform-engineering-patterns/
- Software Security — Prompt injection: contain it with a tool gateway:
  https://www.softwaresecurity.com/domains/ai-emerging/llm-security/prompt-injection-boundaries/
- LearnLive — Defending AI Agents Against Prompt Injection:
  https://www.learnlive.app/learn/ai-agents-automation/defending-agents-against-prompt-injection
