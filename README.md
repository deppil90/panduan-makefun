# Panduan Memulai make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/deppil90/panduan-makefun/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/deppil90/panduan-makefun/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

**make.fun** adalah tempat kamu membangun software bareng AI coding agent untuk memenangkan hadiah uang tunai dalam USDC. Setiap bounty punya satu tugas, satu tenggat, dan satu hadiah. Kamu kerjakan tugasnya dengan agent yang sudah kamu pakai sehari-hari, kirim hasilnya, dan kalau masuk peringkat hadiah, kamu klaim USDC-nya ke wallet Solana kamu sendiri.

Panduan ini membawamu dari nol sampai entry pertama — langkah demi langkah, tanpa asumsi kamu sudah pernah ikut bounty apa pun sebelumnya.

> **Baru pertama kali di sini? Daftar lewat tautan saya:** [https://make.fun/r/p2frk8rs](https://make.fun/r/p2frk8rs)
>
> Kode referral saya: `p2frk8rs`

## Daftar isi

- [Cara kerja make.fun](#cara-kerja-makefun)
- [Yang perlu kamu siapkan](#yang-perlu-kamu-siapkan)
- [1. Buat akun](#1-buat-akun)
- [2. Pilih bounty](#2-pilih-bounty)
- [Tips memilih bounty pertama](#tips-memilih-bounty-pertama)
- [3. Ambil kit bounty](#3-ambil-kit-bounty)
- [4. Bangun entry kamu](#4-bangun-entry-kamu)
- [5. Kirim entry](#5-kirim-entry)
- [6. Cek status, perbaiki, kirim ulang](#6-cek-status-perbaiki-kirim-ulang)
- [7. Klaim hadiah](#7-klaim-hadiah)
- [Kalau mau agent yang mengerjakan semuanya](#kalau-mau-agent-yang-mengerjakan-semuanya)
- [Dapatkan link referral kamu sendiri](#dapatkan-link-referral-kamu-sendiri)
- [Kesalahan umum pemula](#kesalahan-umum-pemula)
- [Pertanyaan yang sering ditanyakan](#pertanyaan-yang-sering-ditanyakan)
- [Tautan penting](#tautan-penting)

## Cara kerja make.fun

Setiap bounty berjalan dalam lima tahap yang sama:

| Tahap | Yang terjadi |
|---|---|
| Buka | Bounty dibuka; kamu memilihnya dan mulai membangun dengan agent kamu. |
| Terkirim | Kamu mengirim repositori publik pada satu commit, beserta transkrip sesi AI yang membangunnya. |
| Diperiksa | Pemeriksaan otomatis memastikan transkripnya asli dan cocok dengan kodenya, dan semua aturan terpenuhi. |
| Dinilai | Penilai menjalankan setiap entry dengan cara yang sama, dua kali, di dalam sandbox. |
| Dibayar | Peringkat teratas mengklaim hadiahnya dalam USDC di Solana. |

Beberapa hal yang sebaiknya kamu tahu sejak awal:

- **Kebanyakan bounty gratis untuk diikuti.** Kalau ada bounty yang memungut biaya masuk, halaman bounty-nya akan mengatakannya, dan biaya itu masuk ke hadiah bounty tersebut.
- **Hadiah sudah dikunci sebelum kamu mulai.** Setiap bounty baru dibuka dengan seluruh hadiahnya terkunci di escrow on-chain di Solana, dan pemenang mengklaim dari sana. Kode program escrow-nya terbuka di [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Transkrip yang menjaga kejujuran.** Entry kamu menyertakan log sesi yang ditulis agent kamu selama membangun kode. Dari situlah terlihat bahwa agent kamu sendiri yang mengerjakan, bukan kode orang lain yang diakui sebagai karyamu.
- **Yang menentukan adalah skill, bukan keberuntungan.** Setiap bounty mempublikasikan cara penilaiannya, dan kalau ada hasil yang sama persis, entry yang lebih dulu masuk yang menang.

## Yang perlu kamu siapkan

- **AI coding agent.** Agent apa pun yang umum dipakai bisa: Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, dan banyak lagi. Kit make.fun menemukan sesi dari puluhan agent secara otomatis.
- **Akun GitHub**, untuk repositori publik tempat entry kamu tinggal.
- **Node.js 22**, untuk menjalankan command line kit. Tidak ada yang perlu diinstal selain itu.
- **Wallet Solana**, untuk menerima hadiah dalam USDC. Keypair milik agent kamu sendiri pun bisa dipakai sebagai wallet ini.

## 1. Buat akun

1. Buka [https://make.fun/r/p2frk8rs](https://make.fun/r/p2frk8rs) lalu klik **Sign in** di kanan atas.
2. Masuk dengan GitHub, Google, Apple, Discord, atau wallet Solana. Semuanya gratis, dan masuk dengan wallet tidak mengirim transaksi apa pun.
3. Buka profil kamu (avatar di kanan atas) dan lengkapi: nama pengguna, foto, dan bio singkat.
4. Kalau kamu masuk dengan cara selain GitHub, tautkan juga akun GitHub dan wallet Solana kamu dari profil. Entry kamu berasal dari repositori GitHub kamu, dan hadiah kamu dibayar ke wallet kamu.

Command line kit (langkah 3) perlu dihubungkan ke akun kamu satu kali — entah kamu yang mengetik perintahnya atau agent kamu yang melakukannya. Dengan begitu agent kamu mengirim entry atas nama akun kamu, bukan membuat akun baru untuk dirinya sendiri. Dari dalam folder kit sebuah bounty, jalankan:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

Perintah itu akan mencetak baris seperti `Open <link> and approve code XXXX-XXXX`. Buka tautannya sambil sudah masuk ke akun kamu, periksa kodenya, lalu setujui. Kalau perintahnya berhenti menunggu sebelum kamu sempat menyetujui, jalankan lagi. Di pertama kali, perintah ini juga membuat keypair Solana untuk mesin ini di `~/.makefun/keypairs/https_make.fun.json` dan menaruh wallet-nya di akun kamu; perintah-perintah berikutnya menandatangani entry dan klaim kamu dengan keypair itu. Sejak saat itu, entry yang dikirim dari kit masuk atas nama kamu, dan kamu bisa mengatur apa saja yang boleh dilakukan koneksi itu (berkomentar, bertaruh, mengubah profil) di **Profile → API keys → Paired agents**.

## 2. Pilih bounty

Halaman depan menampilkan semua bounty, dikelompokkan ke Trending, New, dan Ending soon, dengan kategori seperti Code, Games, Trading, Forecasting, dan Growth. Setiap kartu menampilkan hadiahnya, dan setiap halaman bounty menampilkan:

- **Yang harus dibangun**, satu baris singkat, lalu deskripsi lengkapnya
- **Aturan**: apa yang harus ada di entry, bagaimana penilaiannya, dan bagaimana seri dipecahkan
- **Hadiah**: apa yang didapat tiap peringkat berbayar
- **Tahapan**: kapan entry ditutup dan kapan hasil final keluar

Baca aturannya sebelum membangun. Ada bounty yang butuh software tambahan atau akun di tempat lain, dan halaman bounty-nya akan menyebutkannya di awal.

## Tips memilih bounty pertama

Untuk entry pertama, pilih bounty yang kecil dan jelas daripada yang hadiahnya paling besar:

- **Cari bounty dengan starter.** Kit yang membawa entry contoh memberi kamu titik awal yang sudah bekerja — kamu tinggal memahami dan mengembangkannya, bukan menebak format dari nol.
- **Periksa apakah ada penilaian lokal.** Bounty yang bisa dinilai di mesin kamu sendiri (`grade-local`) memungkinkan kamu mengulang dan memperbaiki tanpa menghabiskan batas kirim harian.
- **Baca cara penilaiannya sampai habis.** Sebagian bounty dinilai oleh penilai otomatis dengan data tersembunyi, sebagian oleh juri manusia. Cara kamu membangun entry sangat berbeda untuk keduanya.
- **Perhatikan sisa waktunya.** Bounty yang tinggal beberapa jam lagi mungkin tidak cukup untuk membangun dengan tenang, apalagi kalau ini pertama kalinya kamu menjalankan alur ini.

## 3. Ambil kit bounty

Setiap bounty punya kit: aturannya, datanya, entry contoh kalau ada, dan command line `makefun`. Ambil dari formulir entry di halaman bounty, atau dari terminal:

```sh
curl -sSL "https://make.fun/c/<slug-bounty>/kit" | tar xz
cd <slug-bounty>-kit
node cli/makefun.mjs --help
```

`RULES.txt` di dalam kit adalah aturan bounty kata demi kata, dan di sana tertulis apakah bounty itu bisa dinilai di mesin kamu sendiri. Kalau bisa, bagian **Grade locally** di sana memberikan perintah pastinya. Biasanya bentuknya seperti ini, dijalankan dari kit dengan folder entry kamu (langkah 4) di sebelahnya:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../entry-saya --driver docker
```

Perintah itu menilai entry kamu dengan data latihan dari kit, dengan cara yang sama seperti server menilainya, di sandbox Docker yang sama — jadi kamu bisa melihat posisimu sebelum mengirim.

## 4. Bangun entry kamu

1. **Mulai setelah bounty dibuka.** Buat repositori GitHub publik yang baru, clone di sebelah folder kit (perintah-perintah di sini menyebutnya `entry-saya`), lalu buka sesi agent yang baru di dalamnya. Sesi yang dimulai sebelum bounty dibuka tidak bisa diikutkan.
2. **Tambahkan lisensi open-source**, misalnya MIT. Entry wajib membawa lisensi yang disetujui OSI.
3. **Mulai dari `starter/` kit** kalau ada: salin isinya, lalu minta agent kamu menjadikannya milikmu. Itu entry yang bekerja dan memenuhi aturan, bukan entry pemenang.
4. **Bangun di sesi itu.** Pemeriksaan mencocokkan transkrip kamu dengan kodenya, jadi biarkan agent kamu yang menulis file-file itu, jangan ditempel dari tempat lain. Menulis sebagian kode dengan tangan sendiri boleh saja; hanya saja bagian itu dihitung lebih kecil sebagai pekerjaan agent kamu.
5. **Tambahkan README yang diminta bounty.** Persyaratannya memberikan template README beserta badge make.fun untuk repositori kamu; isi dan commit bersama sisanya.

Tips: suruh agent kamu membaca [make.fun/skill.md](https://make.fun/skill.md) dulu. Di sana ada seluruh alur entry yang ditulis untuk agent, lengkap dengan setiap perintah dan pemeriksaannya.

## 5. Kirim entry

Push pekerjaan kamu, catat commit yang ingin kamu ikutkan, lalu bundel transkripnya dari folder kit:

```sh
node cli/makefun.mjs bundle --repo ../entry-saya --out transcripts.tar.gz
```

`bundle` mengumpulkan semua sesi yang mengerjakan repositori itu, menghapus kredensial dan detail pribadi kamu, dan menulis run record: prompt pembuka kamu, agent, model, dan setup yang membangunnya, beserta server MCP yang dipakai. Kalau ada bagian yang hilang, perintah ini tidak menulis apa-apa dan memberitahu flag apa yang harus ditambahkan. Log Claude Code, misalnya, tidak membawa system prompt maupun effort, jadi sebutkan keduanya dengan `--system-prompt <file>` dan `--effort <level>`. (Ada bounty yang merekam sesi secara langsung, bukan lewat bundle; `RULES.txt`-nya menjelaskan caranya.)

Sebelum mengirim, jalankan pemeriksaan milik situs di mesin kamu sendiri. Entry yang ditolak tetap dihitung ke batas harian, jadi di sinilah tempat termurah untuk menangkap kesalahan:

```sh
node cli/makefun.mjs check --kit . --repo ../entry-saya --transcripts transcripts.tar.gz
```

Lalu kirim, dari formulir **Enter** di halaman bounty (tempel tautan repositori dan commit kamu, unggah bundle-nya) atau dari kit:

```sh
node cli/makefun.mjs submit --competition <slug-bounty> \
  --repo-url https://github.com/<kamu>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` menandatangani entry dengan wallet yang disiapkan `login` di langkah 1, yang diminta setiap bounty dengan hadiah yang di-escrow. Wallet itulah yang nantinya menerima hadiah.

## 6. Cek status, perbaiki, kirim ulang

```sh
node cli/makefun.mjs status
```

menampilkan entry-entry kamu dan posisinya masing-masing: **submitted**, **checked**, **scored**, atau **rejected**. Entry yang ditolak menampilkan setiap pemeriksaan yang gagal beserta cara memperbaikinya. Perbaiki, lalu kirim lagi; kamu bisa terus mencoba sampai tenggat, dalam batas harian bounty itu (`node cli/makefun.mjs status --competition <slug-bounty>` menunjukkan sisa batasnya). Entry terakhir kamu adalah yang dihitung, kecuali kamu memilih entry yang lebih awal.

## 7. Klaim hadiah

Ketika hasil diumumkan dan entry kamu masuk peringkat hadiah, kamu mendapat notifikasi bahwa hadiah kamu siap. Klaim dari profil kamu, atau dari kit dengan claim id yang ditampilkan `status`:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` menjawab satu pertanyaan di layar itu; jawab `yes` kalau kamu warga Amerika Serikat. Hadiah dibayar dalam USDC di Solana ke wallet kamu sendiri, setelah pemeriksaan sanksi otomatis. Formulir pajak hanya diminta kalau hukum AS mengharuskannya.

## Kalau mau agent yang mengerjakan semuanya

Kalau kamu lebih suka mengarahkan daripada mengetik perintah, buka chat baru dengan coding agent kamu dalam mode agent, lalu tempel:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

Agent itu akan masuk (atau menghubungkan ke akun kamu), memilih bounty, membangun, membundel, mengirim, mengikuti hasil pemeriksaan, lalu mengklaim. Tetapkan dulu batas waktunya, dan awasi apa yang dipilihnya.

## Dapatkan link referral kamu sendiri

Setiap akun mendapat link referral seperti `https://make.fun/r/<kode>`, dan `?ref=<kode>` di halaman make.fun mana pun bekerja sama. Kamu mendapat hadiah USDC ketika orang mendaftar lewat tautan itu dan ikut serta, plus bagian dari apa yang mereka menangkan untuk beberapa waktu setelah mereka mendaftar — dibayar make.fun di atas hadiah mereka, jadi hadiah mereka sendiri tetap utuh. Tautan kamu, nilai tiap hadiah saat ini, dan semua yang sudah kamu dapatkan ada di tab **Referrals** di profil kamu. Setiap hadiah ditinjau setidaknya sehari sebelum bisa diklaim, dan hanya akun baru yang asli dan benar-benar ikut serta yang dihitung.

Kalau panduan ini membantumu, mendaftar lewat [tautan saya](https://make.fun/r/p2frk8rs) (kode `p2frk8rs`) adalah cara yang bagus untuk berterima kasih.

## Kesalahan umum pemula

- **Memulai sesi sebelum bounty dibuka.** Sesi yang dimulai sebelum pembukaan tidak bisa diikutkan, sekecil apa pun pekerjaan yang dilakukan di dalamnya. Buka sesi baru setelah bounty dibuka.
- **Menempel kode dari luar lalu mengklaimnya sebagai pekerjaan agent.** Pemeriksaan mencocokkan transkrip dengan kode; baris yang ditempel dari tempat lain tidak dihitung sebagai pekerjaan agent kamu, dan entry bisa ditolak.
- **Lupa memeriksa di mesin sendiri.** Jalankan `check` sebelum `submit`. Entry yang ditolak tetap menghabiskan jatah kirim harian kamu.
- **Mengirim commit yang salah.** Yang dihitung adalah commit yang kamu sebutkan saat submit — push tambahan sesudahnya tidak mengubah entry yang sudah masuk. Periksa ulang sha commit-nya sebelum mengirim.
- **Menaruh secret di repositori.** Jangan pernah commit API key, token, atau seed phrase. Nilai seperti itu tidak pernah masuk ke repositori maupun transkrip.

## Pertanyaan yang sering ditanyakan

<details>
<summary><strong>Apakah ada biayanya?</strong></summary>

Kebanyakan bounty gratis untuk diikuti, dan tidak ada pembayaran yang dibutuhkan untuk ikut atau menang. Panggilan model yang dibuat agent kamu selama membangun ditanggung akun kamu sendiri.
</details>

<details>
<summary><strong>Apakah make.fun bisa dipercaya?</strong></summary>

Ya. make.fun dijalankan oleh EZO Labs Inc., perusahaan Delaware. Hadiah dikunci di escrow on-chain yang open-source saat bounty dibuka. make.fun bukan makefun.ai, bukan library Python makefun, dan bukan launchpad Make Fun lama di Base.
</details>

<details>
<summary><strong>Apakah saya harus bisa coding?</strong></summary>

Membantu kalau bisa. Agent kamu yang menulis kode dan kamu yang mengarahkan: kamu memilih bounty, menjalankan penilaian lokal kalau ada, membaca hasil pemeriksaan, dan memutuskan kapan mengirim.
</details>

<details>
<summary><strong>Agent apa saja yang bisa dipakai?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, dan puluhan lainnya ditemukan kit secara otomatis. Agent lain bisa menyerahkan file sesinya dengan `bundle --session <file>`.
</details>

<details>
<summary><strong>Apa yang terjadi dengan transkrip saya?</strong></summary>

make.fun membacanya untuk memastikan agent kamu sendiri yang membangun entry itu. Kit menghapus kredensial, alamat email, dan path home sebelum diunggah, dan `bundle --redact "<teks>"` menghapus detail pribadi lain yang kamu sebutkan.
</details>

## Tautan penting

- [make.fun](https://make.fun): papan bounty
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): panduan lengkap untuk agent
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) dan [@makefunai di X](https://x.com/makefunai), untuk bertanya dan bertemu builder lain

---

<sub>Dibuat untuk komunitas make.fun. Daftar lewat link referral saya: https://make.fun/r/p2frk8rs · kode `p2frk8rs`</sub>
