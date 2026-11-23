# SQMC — Standard Quality Mutu Controller

Web app pengendali mutu untuk industri manufaktur (contoh awal: **sambungan pipa / fitting**).
Satu file `index.html`, tanpa build step, siap di-deploy ke Vercel / GitHub Pages / hosting statis apa pun.

## Antarmuka (v1.1)

- **Logo & identitas** sesuai brand SQMC (simbol vektor SVG + wordmark), favicon, dan header PDF berlogo.
- **UI shell ala IBM Carbon:** header putih 56 px, panel navigasi kiri dikelompokkan per tahap PDCA (Plan / Do / Check & Act / Referensi), dan menu hamburger di layar < 1056 px.
- **Pola SAP Fiori:** *dynamic page header* dengan breadcrumb, *launchpad tiles* di Beranda, *object page anchor bar* pada hasil spesifikasi, dan *analytical list page* (panel konfigurasi sticky + konten analisis) pada Peta Kendali.
- **Komponen gaya Carbon:** field input, data table, inline notification, tag, dan progress indicator. Palet warna diambil dari logo (navy `#0A1F44`, biru `#1E7AE5`, abu `#DFE3E7`).

## Fitur

| Menu | Fungsi |
|---|---|
| **Spesifikasi Standar** | Input produk (dropdown + isian bebas): jenis fitting, material, bahan baku, % daur ulang, berat bersih/unit, proses, sambungan, PN, suhu, lingkungan pemakaian (tanah/air tawar/laut/UV/kimia), fluida, dan dimensi kritis. Output: standar acuan (ISO/SNI/ASME/ASTM/EN) beserta alasan & tautan resmi, peringatan kecocokan material, toleransi berat & dimensi (LSL/USL), rencana sampling AQL ISO 2859-1, katalog cacat + disposisi (terima / rework-finishing / tolak), rencana uji, dan **PDF Lembar Spesifikasi**. |
| **Kalkulator disposisi** | Keputusan per unit cacat: terima, boleh finishing (rework), atau tolak, berdasarkan syarat (lokasi non-fungsional, dimensi pasca-finishing, tebal dinding minimum, dsb.). |
| **Input Data** | Basis data pengukuran di sistem: dataset variabel (subgrup n) & atribut (diperiksa/cacat), tempel dari Excel, ekspor CSV, cadangan JSON. |
| **Peta Kendali** | Unggah CSV/XLSX, pakai dataset sistem, atau tempel data. Peta I-MR, X̄-R, X̄-S, P, NP, C, U; 8 tes pola (Western Electric/Nelson, setara Minitab); Fase I (kecualikan subgrup) & μ/σ historis; kapabilitas Cp/Cpk/Pp/Ppk + PPM + normalitas Anderson-Darling; ekspor PNG, CSV, dan **laporan PDF**. |
| **Pustaka Standar** | 50+ standar dengan ruang lingkup (parafrase), tautan katalog resmi, dan ringkasan PDF. |

## Catatan penting

- **Dokumen standar resmi tidak disertakan.** ISO/SNI/ASME/ASTM/EN berhak cipta dan dijual oleh penerbitnya. SQMC menautkan ke halaman resmi dan membuat *ringkasan* PDF sendiri.
- **Status edisi (dicek ke katalog resmi, Nov 2026):** 46 berlaku, 7 berlaku tetapi sedang direvisi (ISO 1452-3, ISO 4427-3, ISO 15874-3, ISO 2531, ISO 4892-2, ISO 6506-1, ISO 21809-1), 1 rancangan (RSNI3 139-2024), 5 edisi belum dapat dipastikan (ASME B1.20.1, ISO 7005-1, ISO/TR 10358, EN 10204, SNI ISO 15874-3). Edisi baru 2025–2026 yang sudah diterapkan: ISO 9001:2026, ISO 2859-1:2026, ISO 22514-2:2026, ISO 10012:2026, ISO 4437-3:2026, ISO 15589-1:2026, ISO 15875-3:2025, ISO 1183-1:2025.
- Toleransi berat default per proses (±1–5%) adalah **rekomendasi internal**, bukan kutipan ISO. Validasi dengan Cpk ≥ 1,33.
- Konstanta d₂/d₃ dihitung numerik (6 desimal); c₄ dihitung eksak via fungsi gamma. Hasil X̄-R, I-MR, P, Cp/Cpk/Ppk, dan AD telah dicocokkan dengan numpy/scipy.

## Penyimpanan data

Urutan: database akun Claude (bila dibuka sebagai artifact claude.ai) → `localStorage` browser → memori sementara.
Saat di-deploy mandiri (Vercel), data tersimpan di browser pengguna. Gunakan **Ekspor cadangan (JSON)** untuk backup/pindah perangkat.

## Deploy ke Vercel

1. Import repo ini di vercel.com → Framework preset: **Other** → tanpa build command, output directory `.`
2. Deploy. `index.html` langsung tersaji.

## Roadmap (PDCA berikutnya)

- Backend + login multi-user (mis. Supabase) agar data dipakai bersama tim QC
- Aturan perpindahan inspeksi normal/ketat/longgar & skip-lot (ISO 2859-1:2026)
- Peta EWMA/CUSUM, Gage R&R (MSA), Pareto cacat
- Master data material & standar yang bisa diedit admin
- Template laporan NCR / 8D dari hasil disposisi
