# PsychoTest Pro

Simulasi psikotes kerja interaktif — latihan Kraepelin/Pauli, tes logika-verbal-spasial, tes kepribadian DISC & PAPI Kostick, hingga simulasi SKD CPNS (TWK/TIU/TKP), lengkap dengan pembahasan dan dashboard hasil bergrafik.

Dibangun sebagai single-file web app (HTML/CSS/JS murni, tanpa build step, tanpa backend) — tinggal di-deploy ke hosting statis mana pun.

## ✨ Fitur

| Modul | Deskripsi |
|---|---|
| **Logika & Angka** | Deret angka & penalaran logis, bank soal khas tes BUMN, timer per soal |
| **Verbal** | Sinonim, antonim, analogi kata |
| **Spasial** | Melanjutkan pola bentuk |
| **Kraepelin / Pauli** | Simulasi "tes koran" — jumlahkan dua angka berurutan, kolom berpindah otomatis, hasil dianalisis 4 indikator (PANK/TIAN/HIEK/POGI) |
| **DISC** | Tes kepribadian pilihan paksa, hasil profil D/I/S/C + kecocokan budaya kerja |
| **PAPI Kostick** | 20 aspek gaya kerja dalam 7 bidang, format pilihan paksa sesuai struktur resmi |
| **SKD CPNS** | Simulasi berurutan TWK → TIU → TKP ala CAT BKN, skor dibandingkan ambang batas resmi (diskalakan proporsional) |

Semua modul menyimpan progres otomatis selama sesi berjalan, punya sistem anti-cheating sederhana (deteksi pindah tab), dan dashboard hasil dengan grafik (Chart.js) serta pembahasan per soal.

## 🚀 Cara deploy

File ini **satu file HTML mandiri** (`psychotest-pro.html`) — tidak perlu `npm install`, tidak perlu server backend.

**Opsi tercepat (drag & drop):**
1. [Netlify Drop](https://app.netlify.com/drop) — seret file HTML ke halaman itu, langsung online.
2. [Vercel](https://vercel.com) — buat project baru, upload file ini sebagai `index.html`.
3. **GitHub Pages** — push ke repo, rename file jadi `index.html`, aktifkan Pages di Settings → Pages.

**Yang perlu diperhatikan:** rename file jadi `index.html` di server, karena kebanyakan static hosting mencari file itu sebagai halaman utama secara default.

## 💾 Soal penyimpanan progres

Fitur "simpan progres otomatis" memakai **dual-storage otomatis**: kode mencoba `localStorage` asli terlebih dulu, dan baru jatuh ke `window.storage` (API penyimpanan bawaan lingkungan artifact Claude) kalau `localStorage` tidak tersedia/diblokir.

Efeknya:
- **Saat masih dites di lingkungan preview Claude**: `localStorage` diblokir platform, jadi otomatis pakai `window.storage` — kadang bisa gagal karena ini bergantung pada layanan pihak Claude, tapi kegagalannya ditangani dengan aman (tidak akan bikin situs error, cuma progres tidak tersimpan lintas kunjungan).
- **Setelah di-deploy ke hosting sungguhan** (Netlify/Vercel/GitHub Pages/dst): `localStorage` otomatis terdeteksi tersedia dan dipakai — ini API browser standar, 100% andal, tidak bergantung server/pihak ketiga mana pun. Tidak perlu ubah kode apa pun lagi.

## 🛠️ Tech stack

- HTML/CSS/JS vanilla — tanpa framework, tanpa build tool
- [Chart.js](https://www.chartjs.org/) (via CDN) — grafik radar Kraepelin
- Google Fonts — Fraunces (display), IBM Plex Mono (data/angka), Inter (body)
- Komponen visual kartu 3D diadaptasi dari [Uiverse.io](https://uiverse.io) (kredit: SmookyDev untuk kartu amplop, imtausef untuk kartu tilt-hover)

## 📁 Struktur

Satu file: `psychotest-pro.html` — HTML, CSS (`<style>`), dan JS (`<script>`) digabung dalam satu berkas untuk portabilitas maksimal.

## 📌 Batasan & catatan kejujuran

- Ini alat **latihan/simulasi**, bukan pengganti tes resmi perusahaan atau instansi. Skor dan persentil bersifat estimasi.
- Modul Kraepelin, DISC, dan PAPI Kostick memakai versi ringkas (jumlah soal/kolom lebih sedikit dari tes asli) untuk kebutuhan latihan cepat.
- Ambang batas SKD CPNS di modul ini **diskalakan proporsional** dari passing grade resmi (Kepmen PANRB No. 321/2024: TWK 65/150, TIU 80/175, TKP 166/225 dari total 110 soal) karena simulasi memakai 30 soal — bukan angka resmi apa adanya. Regulasi bisa berubah; selalu cek sumber resmi BKN/PANRB untuk info terbaru.

## 🗺️ Roadmap (opsional, lanjutan)

Ide pengembangan berikutnya yang belum dikerjakan:
- Modul EPPS dan CFIT (psikotes populer lain)
- Leaderboard/papan peringkat bersama antar pengguna
- Progress tracking lintas-sesi (grafik perkembangan dari waktu ke waktu)
- Backend & akun pengguna sungguhan (lihat PRD awal untuk skema database)

---

*Dibuat dengan Claude.*
