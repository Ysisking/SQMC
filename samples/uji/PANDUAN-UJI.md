# Paket Data Uji SQMC + Kunci Jawaban

Semua angka kunci jawaban dihasilkan oleh mesin SQMC lalu dicek silang dengan numpy/scipy.
Pemisah desimal di layar SQMC memakai koma (format Indonesia). Tes pola default yang dipakai: semua (1–8).

---

## A. Menu Peta Kendali, unggah file

| # | File | Pengaturan yang perlu diubah | Hasil yang seharusnya muncul |
|---|---|---|---|
| 01 | `01_xbar-r_berat_STABIL.csv` | LSL 37,73 · USL 39,27 · Target 38,5 | **X̄-R** otomatis (n=5, 25 subgrup). X̄: UCL 38,6687 · X̄ 38,5038 · LCL 38,3388. R: UCL 0,6047 · R̄ 0,2860 · LCL 0. **Tidak ada titik gagal tes lalu proses terkendali.** Cp 2,09 · Cpk 2,08 · Pp 2,19 · Ppk 2,18. AD p = 0,900 (normal). |
| 02a | `02_xbar-r_berat_BERGESER.csv` | LSL/USL seperti 01 | X̄: UCL 38,7219 · X̄ 38,5567 · LCL 38,3915. Gagal tes: subgrup **8** (Tes 1), **21** (Tes 5), **23** (Tes 6), **25** (Tes 1, 6). |
| 02b | file yang sama | + *Opsi estimasi* lalu kecualikan `8, 18-25` | Batas dihitung ulang dari data yang stabil saja: UCL 38,6741 · X̄ 38,4943 · LCL 38,3144. Pergeseran mulai subgrup 18 kini terlihat jelas: **8** (T1), **20** (T1), **21** (T1, 5, 6), **22–23** (T5, 6), **24** (T6), **25** (T1, 2, 5, 6, 8). Cpk 1,90. |
| 03 | `03_imr_diameter-socket_TREN.csv` (pemisah `;`, desimal koma) | Ukuran subgrup = **1** · LSL 20,10 · USL 20,40 · Target 20,20 · kecualikan `33-40` | **I-MR**. I: UCL 20,2660 · X̄ 20,2184 · LCL 20,1708. MR: UCL 0,0585 · MR̄ 0,0179. Tren naik (keausan cetakan): **35** (T3), **36** (T1, 3, 5), **37–39** (T1, 3, 5, 6), **40** (T1, 2, 3, 5, 6). Cpk 2,49, capable, tapi **tidak stabil**, jadi indeks ini belum sah. |
| 04 | `04_xbar-s_tebal-dinding_n10_FORMAT-PANJANG.csv` | Struktur lalu **"Satu kolom nilai + kolom ID subgrup"**, kolom ID = `subgrup` · LSL 2,20 · USL 2,40 · Target 2,30 | **X̄-S** otomatis (n=10, 20 subgrup). X̄: UCL 2,3380 · X̄ 2,3029 · LCL 2,2679. S: UCL 0,0617 · S̄ 0,0360 · LCL 0,0102. Tidak ada titik gagal tes, **tetapi Cp 0,90 · Cpk 0,87, ±7.018 PPM** lalu proses **stabil tapi tidak capable** (variasi terlalu lebar untuk toleransi ±0,10). |
| 05 | `05_p-chart_cacat-visual_N-BERVARIASI.csv` | Tanpa pengaturan (terdeteksi otomatis sebagai atribut lalu P) | **P chart**, batas berbentuk tangga karena ukuran sampel bervariasi. p̄ = 0,03645 (3,65%). Gagal tes: sampel **12** (Tes 1). |
| 06 | `06_np-chart_unit-cacat_N-TETAP-200.csv` | Jenis peta lalu **NP** | n·p̄ = 10,76 · UCL 20,33 · LCL 1,19. Kenaikan cacat mulai sampel 19: **19** (T1), **21** (T5), **23–24** (T6), **25** (T1, 5, 6). Sampel 13 (T5) adalah *false alarm* yang wajar terjadi saat 8 tes diaktifkan sekaligus. |
| 07 | `07_c-chart_jumlah-cacat-per-batch.csv` | Tanpa pengaturan (otomatis **C**, tidak ada kolom ukuran sampel) | c̄ = 6,68 · UCL 14,43 · LCL 0. Gagal tes: batch **21** (Tes 1). |
| 08 | `08_u-chart_cacat-per-unit.csv` | Tanpa pengaturan (otomatis **U**) | ū = 0,2776 cacat/unit, batas bervariasi. Gagal tes: sampel **7** (Tes 1). |
| 10 | `10_SQMC_contoh-uji_MULTI-SHEET.xlsx` | Pilih sheet **Berat_XbarR** / **Diameter_IMR** / **Cacat_P** | Sheet *Berat_XbarR* = data 02 (hasil sama dengan 02a). *Diameter_IMR* = data 03. *Cacat_P* = data 05. Gunanya menguji pemilihan sheet. |

**Cek tambahan di setiap file:** tombol **PNG**, **Laporan PDF**, **CSV hasil**; arahkan kursor (tap) ke titik merah untuk melihat nomor tes.

---

## B. Menu Input Data, tempel dari Excel

1. **Input Data** lalu **Dataset variabel** lalu nama bebas, ukuran subgrup **5**.
2. **Tempel dari Excel** lalu salin seluruh isi `09_TEMPEL-ke-Input-Data.txt` lalu **Tambahkan**.
3. Hasil: **10 baris** bertanggal 27 Nov – 6 Des 2026, nilai berkoma desimal terbaca benar.
4. Isi LSL 37,73 / USL 39,27 lalu **Simpan** lalu **Analisis**. Uji juga **CSV**, **Ekspor cadangan (JSON)** lalu **Impor cadangan**.

---

## C. Menu Spesifikasi Standar, 5 skenario

| # | Isian utama | Yang harus muncul |
|---|---|---|
| S1 | Elbow 90° · **PVC-U** · solvent cement · injeksi · berat **38,5** g · PN 10 · suhu 30 °C · lingkungan: tanah + udara terbuka · fluida: air minum · daur ulang **5%** internal · dimensi "Diameter dalam socket" 20,2 (+0,2 / −0,1) · lot 1000, level II, AQL 1,0 / 2,5 | Standar produk: **ISO 1452-3:2009**, **SNI 06-0135-1987**. Peringatan: UV (⚠), material rework (⚠), kontak air minum (ℹ), derating PN (ℹ). Berat 37,73 – 39,27 g (±2%). Socket 20,10 – 20,40. Sampling: Kritis **J lalu L** n=200 Ac0/Re1 · Mayor **J** n=80 **Ac2/Re3** · Minor n=80 **Ac5/Re6**. |
| S2 | Tee · **PP-R** · socket fusion · 42 g · toleransi kustom **±1,5%** · PN 20 · suhu **75 °C** · dalam ruangan · air panas · lot 3000, AQL 0,65 / 1,5 | **ISO 15874-3:2013**, **SNI ISO 15874-3**, ISO 10508. ⚠ suhu 75 °C > 70 °C (cek kelas aplikasi). Berat 41,37 – 42,63 g. Mayor **K** n=125 Ac2/Re3 · Minor Ac5/Re6. |
| S3 | Elbow · **Besi cor maleabel** · ulir tirus ISO 7-1 · casting · 180 g · lapisan **tidak** dicentang · tanah + air laut · dimensi "Panjang center-to-end" 28 mm ISO 2768-1 kelas **c** · lot 500 | **ISO 49:1994**, RSNI3 139-2024, ISO 7-1, ISO 7-2, ISO 12944-2:2017, ISO 15589-1, ISO 8062-3. ⚠ logam tertanam tanpa lapisan, besi cor di air laut tanpa lapisan. Berat 171 – 189 g (±5%). Dimensi 27,5 – 28,5 mm (±0,5). Mayor **H** n=50 Ac1/Re2. |
| S4 | **Uji negatif**: Socket · PVC-U · 25 g · suhu **60 °C** · fluida **gas + air panas** · daur ulang **20% eksternal** · lot 200 | **Empat** peringatan merah: suhu > 45 °C, PVC-U bukan untuk air panas, tidak sesuai untuk gas, daur ulang eksternal. Kritis n=200 = **100% inspeksi**. Mayor **G lalu H** n=50 Ac1/Re2. |
| S5 | Elbow · **SS 304** · butt-weld · forming · 520 g · toleransi kustom **±10 g** · air laut + udara terbuka · dimensi OD 60,3 ISO 2768-1 kelas **m** · lot 150, AQL 0,65 / 2,5 | **ASME B16.9**, **ASTM A403**, ASTM A967, ISO 12944-2, ISO 9223. ⚠ SS304 rentan pitting di air laut lalu sarankan 316/316L. Berat 510 – 530 g. OD 60,0 – 60,6 mm (±0,3). Kritis 100% (n ≥ lot) · Mayor **F** n=20 Ac0/Re1 · Minor **F** n=20 Ac1/Re2. |

**Cek tambahan:** **Simpan** lalu muncul di daftar · **Unduh PDF** (5 bagian + kolom pengesahan) · **Kalkulator disposisi** (pilih "Flash / sirip", centang semua syarat lalu *REWORK / FINISHING DIIZINKAN*; hilangkan satu centang lalu *TOLAK*) · **Buat dataset SPC** lalu LSL/USL berat otomatis terisi.

---

## D. Modul v1.3 (MSA, EWMA/CUSUM, Pareto, PFMEA, Control Plan, NCR)

| # | File / langkah | Pengaturan | Hasil yang seharusnya muncul |
|---|---|---|---|
| 11 | **MSA & Kalibrasi lalu Gage R&R** lalu unggah `11_msa_gage-rr_10part-3op-3ulangan.csv` | Kolom terdeteksi otomatis (part, operator, ulangan_1–3) · LSL 9,5 · USL 10,5 | 10 part × 3 operator × 3 ulangan = 90. Interaksi P×O **p = 0,875 lalu digabung**. GRR: %Kontribusi 1,57 · **%Study Var 12,53** · **%Toleransi 19,61** lalu *diterima bersyarat*. Repeatability %SV 10,93 · Reproducibility %SV 6,12 (operator p = 0,0001). Part-to-part %SV 99,21. **ndc = 11**. Interpretasi: repeatability dominan. |
| 12 | **MSA lalu Type-1** lalu unggah `12_msa_type1_50-ukur_ref-25.csv` | Referensi 25,000 · LSL 24,95 · USL 25,05 · resolusi 0,001 · K 20% | n = 50 · rata-rata 25,00068 · s 0,00177 · **Cg 1,88 · Cgk 1,75 lalu layak**. Bias 0,00068, t = 2,726, **p = 0,009 lalu bias signifikan** (kecil, tetapi nyata). Resolusi 1,0% toleransi ✓. |
| 13 | **Analisis Pareto lalu Tempel / unggah** lalu `13_pareto_jenis-cacat_dan-biaya.csv` | Urut **jumlah** | 8 kategori, total 114. Vital few = Flash (40,4%), Short shot (58,8%), Sink mark (73,7%), Dimensi socket (84,2% kumulatif). |
| 13b | file yang sama | Urut **biaya (COPQ)** | Sink mark & belang warna (biaya 0) keluar dari diagram. Vital few = **Short shot** Rp 178.500 (46,8%), **Dimensi socket** Rp 102.000 (73,5%), **Flash** Rp 55.200 (87,9%), urutan berbeda dari Pareto frekuensi. |
| 14a | **Peta Kendali** lalu `14_ewma-cusum_diameter_PERGESERAN-KECIL.csv` | Ukuran subgrup **1** · *Opsi estimasi*: μ historis **20,2**, σ historis **0,02** · jenis peta **I-MR**, tes pola **hanya tes 1** | Tidak ada titik di luar batas I (UCL 20,26 · LCL 20,14), peta Shewhart **tidak menangkap** pergeseran +0,75σ yang dimulai di observasi 21. (Bila 8 tes aktif, hanya obs. 27 tertangkap Tes 6.) |
| 14b | file & opsi sama | Jenis peta **EWMA** (λ 0,2 · L 3) | Sinyal EWMA di observasi **27** dan **38**. UCL akhir 20,22. |
| 14c | file & opsi sama | Jenis peta **CUSUM** (k 0,5 · h 4) | h·σ = 0,08. C⁺ melewati batas di observasi **27** lalu terus-menerus **33–40** lalu pergeseran naik yang persisten. C⁻ tidak ada sinyal. |
| 15 | **Spesifikasi** (skenario S1) lalu simpan lalu **PFMEA lalu Dari spesifikasi** | Baris 1 (Retak, S = 8): isi O = 6, D = 6. Baris 2 (Short shot, S = 8): O = 3, D = 7 | 14 mode kegagalan terisi dari katalog cacat plastik. AP baris 1 = **H**, baris 2 = **M**. Strip ringkasan: 1 High, 1 Medium, 1 "H tanpa tindakan". Uji AP lain: (9,2,5) = M · (7,4,7) = H · (5,4,5) = L · (3,9,9) = M. |
| 16 | PFMEA lalu **Buat Control Plan** | Tanpa pengaturan | Pindah ke Control Plan berisi ±10 karakteristik: bahan baku (10), parameter proses, berat bersih & dimensi dengan X̄-R (20), uji tekanan/oven/visual dengan sampling AQL (30), uji tipe (40), plus baris PFMEA ber-AP H. Pilih fase **Safe Launch** lalu muncul pemberitahuan kendali tambahan. |
| 17 | **NCR & 8D lalu NCR baru** | Pilih spesifikasi S1 lalu jenis cacat "Bocor…" · qty NC 37 · scrap 30 + rework 7 | Kelas otomatis **Kritis**, produk terisi, petunjuk "Total terdisposisi 37 dari 37 ✓". Laporan 8D PDF hanya memuat butir yang diisi. NCR ini lalu muncul di **Pareto lalu Register NCR**. |
| 18 | **MSA lalu Register alat ukur** | Tambah JS-01 (kalibrasi 15-10-2025, 12 bln), TB-02 (01-06-2026, 6 bln), MK-03 (20-09-2026, 12 bln) | Per 26-11-2026: JS-01 **Terlambat** (jatuh tempo 15-10-2026), TB-02 **≤ 30 hari** (01-12-2026), MK-03 **Valid**. Beranda lalu Status mutu menampilkan "1 terlambat". |

## E. Explain dan Deep Analyst (v1.5)

| # | Langkah | Hasil yang seharusnya muncul |
|---|---|---|
| 19 | Peta Kendali, Muat data contoh, lalu Deep Analyst | Dugaan perubahan input proses sekitar subgrup 18 sampai 19 dengan dukungan kuat karena cocok dengan cerita contoh (lot resin baru 19 November). Dugaan variasi dalam subgrup pada subgrup 10 juga berdukungan kuat karena tanggalnya disebut di cerita. Fakta netral untuk shift dan operator (ANOVA tidak bermakna). |
| 20 | Klik Unduh PDF di Deep Analyst | PDF berisi temuan cerita, tabel fakta, keterangan pengguna, dugaan, diagram fishbone, dan langkah verifikasi. |
| 21 | MSA, Muat data contoh, Explain, isi "Alat ukur belum dikalibrasi ulang.", lalu Simpan dan jalankan Deep Analyst | Dugaan bias alat dan alat lewat jatuh tempo kalibrasi naik ke dukungan kuat. Tombol Explain bertanda titik biru. |
| 22 | Deep Analyst tanpa data (mis. Peta Kendali sebelum dijalankan) | Pesan bahwa peta kendali perlu dijalankan terlebih dulu, dengan tombol Isi Explain. |
| 23 | Beranda, Deep Analyst | Ringkasan jumlah dugaan dan catatan kualitas data per modul. |

