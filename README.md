# SQMC — Standard Quality Mutu Controller

Web app pengendali mutu untuk industri manufaktur (contoh awal: **sambungan pipa / fitting**).
Satu file `index.html`, tanpa build step, siap di-deploy ke Cloudflare Pages / GitHub Pages / hosting statis apa pun.

## Antarmuka

- **Logo & identitas** sesuai brand SQMC (simbol vektor SVG + wordmark), favicon, dan header PDF berlogo.
- **UI shell ala IBM Carbon:** header putih 56 px, panel navigasi kiri dikelompokkan per tahap PDCA (Plan / Do / Check / Act / Referensi), dan menu hamburger di layar < 1056 px.
- **Pola SAP Fiori:** *dynamic page header* dengan breadcrumb, *launchpad tiles* di Beranda, *object page anchor bar* pada hasil spesifikasi, dan *analytical list page* (panel konfigurasi sticky + konten analisis) pada Peta Kendali.
- **Komponen gaya Carbon:** field input, data table, inline notification, tag, dan progress indicator. Palet warna diambil dari logo (navy `#0A1F44`, biru `#1E7AE5`, abu `#DFE3E7`).

## Fitur

| Menu | Fungsi |
|---|---|
| **Spesifikasi Standar** | Input produk (dropdown + isian bebas): jenis fitting, material, bahan baku, % daur ulang, berat bersih/unit, proses, sambungan, PN, suhu, lingkungan pemakaian (tanah/air tawar/laut/UV/kimia), fluida, dan dimensi kritis. Output: standar acuan (ISO/SNI/ASME/ASTM/EN) beserta alasan & tautan resmi, peringatan kecocokan material, toleransi berat & dimensi (LSL/USL), rencana sampling AQL ISO 2859-1, katalog cacat + disposisi (terima / rework-finishing / tolak), rencana uji, dan **PDF Lembar Spesifikasi**. |
| **Kalkulator disposisi** | Keputusan per unit cacat: terima, boleh finishing (rework), atau tolak, berdasarkan syarat (lokasi non-fungsional, dimensi pasca-finishing, tebal dinding minimum, dsb.). |
| **Input Data** | Basis data pengukuran di sistem: dataset variabel (subgrup n) & atribut (diperiksa/cacat), tempel dari Excel, ekspor CSV, cadangan JSON. |
| **Peta Kendali** | Unggah CSV/XLSX, pakai dataset sistem, atau tempel data. Peta I-MR, X̄-R, X̄-S, **EWMA (ISO 7870-6:2024)**, **CUSUM tabular (ISO 7870-4:2021)**, P, NP, C, U; 8 tes pola (Western Electric/Nelson, setara Minitab); Fase I (kecualikan subgrup) & μ/σ historis; kapabilitas Cp/Cpk/Pp/Ppk + PPM + normalitas Anderson-Darling; ekspor PNG, CSV, dan **laporan PDF**. |
| **PFMEA** *(v1.3)* | Process FMEA 7 langkah AIAG & VDA (2019): S/O/D 1–10, **Action Priority H/M/L otomatis** (bukan RPN), kolom karakteristik khusus CC/SC, tindakan, PIC, penilaian ulang S′/O′/D′. Bisa diisi otomatis dari katalog cacat spesifikasi. Ekspor CSV & PDF. |
| **Control Plan** *(v1.3)* | Disusun otomatis dari spesifikasi (+ PFMEA): penerimaan bahan baku, proses (SPC berat & dimensi), inspeksi akhir (sampling ISO 2859-1), uji tipe, lengkap dengan rencana reaksi. Kolom & fase (Prototype, Pre-Launch, **Safe Launch**, Production) mengikuti AIAG Control Plan edisi 1 (2024). |
| **MSA & Kalibrasi** *(v1.3)* | **Gage R&R crossed metode ANOVA** (AIAG MSA edisi 4): tabel ANOVA ± interaksi, komponen varians, %Kontribusi, %Study Var, %Toleransi, %Proses, ndc, 4 grafik. **Studi Type-1** Cg/Cgk + uji bias + cek resolusi (≤ 5% VDA 5 / ≤ 10% AIAG). **Register alat ukur** dengan jatuh tempo kalibrasi (ISO 10012, laboratorium ISO/IEC 17025). |
| **Analisis Pareto** *(v1.3)* | Dari register NCR atau CSV/tempel; urut frekuensi atau biaya (COPQ), garis 80%, penanda *vital few*, ekspor PNG/CSV/PDF. |
| **NCR & 8D** *(v1.3)* | Register produk tidak sesuai (status, umur, lewat target), disposisi (use-as-is/konsesi, rework, repair, regrade, scrap, retur) dengan cek keseimbangan qty, alur 8D D0–D8: 5W2H, containment, diagram 6M, 5-Why, titik lolos, verifikasi efektivitas, pencegahan berulang. Laporan 8D PDF. |
| **Pustaka Standar** | 65 standar dengan ruang lingkup (parafrase), tautan katalog resmi, dan ringkasan PDF. |

## Catatan penting

- **Standar baru di v1.3 (dicek Nov 2026):** ISO 7870-4:2021, ISO 7870-6:2024, ISO 22514-7:2026 (edisi ke-3, Sep 2026), ISO/IEC 17025:2017 (dikonfirmasi 2023), IATF 16949:2016 (Revisi 2 sedang disusun), AIAG MSA edisi 4 (2010), VDA 5 edisi 3 (2021), AIAG & VDA FMEA Handbook (2019, errata 2020), AIAG Control Plan edisi 1 (2024), AIAG APQP edisi 3 (2024), AIAG CQI-20 edisi 2 (2018).
- **Validasi numerik v1.3:** Gage R&R ANOVA (p-value F, komponen varians, %SV, %Tol, ndc; 3 skenario termasuk interaksi signifikan), Type-1 (Cg, Cgk, uji t), EWMA, dan CUSUM dicocokkan dengan numpy/scipy — selisih < 1e-9.
- Nilai awal Severity dari katalog cacat, teks rencana reaksi Control Plan, dan target NCR adalah **saran awal SQMC**; keputusan akhir milik tim lintas fungsi.

- **Dokumen standar resmi tidak disertakan.** ISO/SNI/ASME/ASTM/EN berhak cipta dan dijual oleh penerbitnya. SQMC menautkan ke halaman resmi dan membuat *ringkasan* PDF sendiri.
- **Status edisi (dicek ke katalog resmi, Nov 2026):** 46 berlaku, 7 berlaku tetapi sedang direvisi (ISO 1452-3, ISO 4427-3, ISO 15874-3, ISO 2531, ISO 4892-2, ISO 6506-1, ISO 21809-1), 1 rancangan (RSNI3 139-2024), 5 edisi belum dapat dipastikan (ASME B1.20.1, ISO 7005-1, ISO/TR 10358, EN 10204, SNI ISO 15874-3). Edisi baru 2025–2026 yang sudah diterapkan: ISO 9001:2026, ISO 2859-1:2026, ISO 22514-2:2026, ISO 10012:2026, ISO 4437-3:2026, ISO 15589-1:2026, ISO 15875-3:2025, ISO 1183-1:2025.
- Toleransi berat default per proses (±1–5%) adalah **rekomendasi internal**, bukan kutipan ISO. Validasi dengan Cpk ≥ 1,33.
- Konstanta d₂/d₃ dihitung numerik (6 desimal); c₄ dihitung eksak via fungsi gamma. Hasil X̄-R, I-MR, P, Cp/Cpk/Ppk, dan AD telah dicocokkan dengan numpy/scipy.

## Penyimpanan data

Urutan: database akun Claude (bila dibuka sebagai artifact claude.ai) → `localStorage` browser → memori sementara.
Saat di-deploy mandiri (Cloudflare Pages), data tersimpan di browser pengguna. Gunakan **Ekspor cadangan semua modul (JSON)** di menu Input Data untuk backup/pindah perangkat (spesifikasi, dataset, PFMEA, Control Plan, NCR, studi MSA, register alat ukur).

## Deploy ke Cloudflare Pages

1. Cloudflare dashboard → **Workers & Pages** → **Create** → **Pages** → **Connect to Git** → pilih repo `SQMC`.
2. Framework preset **None**, build command dikosongkan, build output directory `/`.
3. Deploy. Setiap push ke `main` otomatis ter-deploy ulang.

## Roadmap (PDCA berikutnya)

- Backend + login multi-user (mis. Supabase) agar data dipakai bersama tim QC
- Aturan perpindahan inspeksi normal/ketat/longgar & skip-lot (ISO 2859-1:2026)
- Master data material & standar yang bisa diedit admin
- MSA atribut (attribute agreement / Kappa), studi bias & linearitas
- Uji kapabilitas data non-normal (transformasi Box-Cox / Johnson)
- PPAP / First Article Inspection & sertifikat inspeksi EN 10204 tipe 3.1
