# Paket Data Uji SQMC + Kunci Jawaban

Semua angka kunci jawaban dihasilkan oleh mesin SQMC lalu dicek silang dengan numpy/scipy.
Pemisah desimal di layar SQMC memakai koma (format Indonesia). Tes pola default yang dipakai: semua (1–8).

---

## A. Menu Peta Kendali — unggah file

| # | File | Pengaturan yang perlu diubah | Hasil yang seharusnya muncul |
|---|---|---|---|
| 01 | `01_xbar-r_berat_STABIL.csv` | LSL 37,73 · USL 39,27 · Target 38,5 | **X̄-R** otomatis (n=5, 25 subgrup). X̄: UCL 38,6687 · X̄ 38,5038 · LCL 38,3388. R: UCL 0,6047 · R̄ 0,2860 · LCL 0. **Tidak ada titik gagal tes → proses terkendali.** Cp 2,09 · Cpk 2,08 · Pp 2,19 · Ppk 2,18. AD p = 0,900 (normal). |
| 02a | `02_xbar-r_berat_BERGESER.csv` | LSL/USL seperti 01 | X̄: UCL 38,7219 · X̄ 38,5567 · LCL 38,3915. Gagal tes: subgrup **8** (Tes 1), **21** (Tes 5), **23** (Tes 6), **25** (Tes 1, 6). |
| 02b | file yang sama | + *Opsi estimasi* → kecualikan `8, 18-25` | Batas dihitung ulang dari data yang stabil saja: UCL 38,6741 · X̄ 38,4943 · LCL 38,3144. Pergeseran mulai subgrup 18 kini terlihat jelas: **8** (T1), **20** (T1), **21** (T1, 5, 6), **22–23** (T5, 6), **24** (T6), **25** (T1, 2, 5, 6, 8). Cpk 1,90. |
| 03 | `03_imr_diameter-socket_TREN.csv` (pemisah `;`, desimal koma) | Ukuran subgrup = **1** · LSL 20,10 · USL 20,40 · Target 20,20 · kecualikan `33-40` | **I-MR**. I: UCL 20,2660 · X̄ 20,2184 · LCL 20,1708. MR: UCL 0,0585 · MR̄ 0,0179. Tren naik (keausan cetakan): **35** (T3), **36** (T1, 3, 5), **37–39** (T1, 3, 5, 6), **40** (T1, 2, 3, 5, 6). Cpk 2,49 — capable, tapi **tidak stabil**, jadi indeks ini belum sah. |
| 04 | `04_xbar-s_tebal-dinding_n10_FORMAT-PANJANG.csv` | Struktur → **"Satu kolom nilai + kolom ID subgrup"**, kolom ID = `subgrup` · LSL 2,20 · USL 2,40 · Target 2,30 | **X̄-S** otomatis (n=10, 20 subgrup). X̄: UCL 2,3380 · X̄ 2,3029 · LCL 2,2679. S: UCL 0,0617 · S̄ 0,0360 · LCL 0,0102. Tidak ada titik gagal tes, **tetapi Cp 0,90 · Cpk 0,87, ±7.018 PPM** → proses **stabil tapi tidak capable** (variasi terlalu lebar untuk toleransi ±0,10). |
| 05 | `05_p-chart_cacat-visual_N-BERVARIASI.csv` | — (terdeteksi otomatis sebagai atribut → P) | **P chart**, batas berbentuk tangga karena ukuran sampel bervariasi. p̄ = 0,03645 (3,65%). Gagal tes: sampel **12** (Tes 1). |
| 06 | `06_np-chart_unit-cacat_N-TETAP-200.csv` | Jenis peta → **NP** | n·p̄ = 10,76 · UCL 20,33 · LCL 1,19. Kenaikan cacat mulai sampel 19: **19** (T1), **21** (T5), **23–24** (T6), **25** (T1, 5, 6). Sampel 13 (T5) adalah *false alarm* yang wajar terjadi saat 8 tes diaktifkan sekaligus. |
| 07 | `07_c-chart_jumlah-cacat-per-batch.csv` | — (otomatis **C**, tidak ada kolom ukuran sampel) | c̄ = 6,68 · UCL 14,43 · LCL 0. Gagal tes: batch **21** (Tes 1). |
| 08 | `08_u-chart_cacat-per-unit.csv` | — (otomatis **U**) | ū = 0,2776 cacat/unit, batas bervariasi. Gagal tes: sampel **7** (Tes 1). |
| 10 | `10_SQMC_contoh-uji_MULTI-SHEET.xlsx` | Pilih sheet **Berat_XbarR** / **Diameter_IMR** / **Cacat_P** | Sheet *Berat_XbarR* = data 02 (hasil sama dengan 02a). *Diameter_IMR* = data 03. *Cacat_P* = data 05. Gunanya menguji pemilihan sheet. |

**Cek tambahan di setiap file:** tombol **PNG**, **Laporan PDF**, **CSV hasil**; arahkan kursor (tap) ke titik merah untuk melihat nomor tes.

---

## B. Menu Input Data — tempel dari Excel

1. **Input Data** → **Dataset variabel** → nama bebas, ukuran subgrup **5**.
2. **Tempel dari Excel** → salin seluruh isi `09_TEMPEL-ke-Input-Data.txt` → **Tambahkan**.
3. Hasil: **10 baris** bertanggal 27 Nov – 6 Des 2026, nilai berkoma desimal terbaca benar.
4. Isi LSL 37,73 / USL 39,27 → **Simpan** → **Analisis**. Uji juga **CSV**, **Ekspor cadangan (JSON)** lalu **Impor cadangan**.

---

## C. Menu Spesifikasi Standar — 5 skenario

| # | Isian utama | Yang harus muncul |
|---|---|---|
| S1 | Elbow 90° · **PVC-U** · solvent cement · injeksi · berat **38,5** g · PN 10 · suhu 30 °C · lingkungan: tanah + udara terbuka · fluida: air minum · daur ulang **5%** internal · dimensi "Diameter dalam socket" 20,2 (+0,2 / −0,1) · lot 1000, level II, AQL 1,0 / 2,5 | Standar produk: **ISO 1452-3:2009**, **SNI 06-0135-1987**. Peringatan: UV (⚠), material rework (⚠), kontak air minum (ℹ), derating PN (ℹ). Berat 37,73 – 39,27 g (±2%). Socket 20,10 – 20,40. Sampling: Kritis **J→L** n=200 Ac0/Re1 · Mayor **J** n=80 **Ac2/Re3** · Minor n=80 **Ac5/Re6**. |
| S2 | Tee · **PP-R** · socket fusion · 42 g · toleransi kustom **±1,5%** · PN 20 · suhu **75 °C** · dalam ruangan · air panas · lot 3000, AQL 0,65 / 1,5 | **ISO 15874-3:2013**, **SNI ISO 15874-3**, ISO 10508. ⚠ suhu 75 °C > 70 °C (cek kelas aplikasi). Berat 41,37 – 42,63 g. Mayor **K** n=125 Ac2/Re3 · Minor Ac5/Re6. |
| S3 | Elbow · **Besi cor maleabel** · ulir tirus ISO 7-1 · casting · 180 g · lapisan **tidak** dicentang · tanah + air laut · dimensi "Panjang center-to-end" 28 mm ISO 2768-1 kelas **c** · lot 500 | **ISO 49:1994**, RSNI3 139-2024, ISO 7-1, ISO 7-2, ISO 12944-2:2017, ISO 15589-1, ISO 8062-3. ⚠ logam tertanam tanpa lapisan, ⛔ besi cor di air laut tanpa lapisan. Berat 171 – 189 g (±5%). Dimensi 27,5 – 28,5 mm (±0,5). Mayor **H** n=50 Ac1/Re2. |
| S4 | **Uji negatif**: Socket · PVC-U · 25 g · suhu **60 °C** · fluida **gas + air panas** · daur ulang **20% eksternal** · lot 200 | **Empat** peringatan ⛔ merah: suhu > 45 °C, PVC-U bukan untuk air panas, tidak sesuai untuk gas, daur ulang eksternal. Kritis n=200 = **100% inspeksi**. Mayor **G→H** n=50 Ac1/Re2. |
| S5 | Elbow · **SS 304** · butt-weld · forming · 520 g · toleransi kustom **±10 g** · air laut + udara terbuka · dimensi OD 60,3 ISO 2768-1 kelas **m** · lot 150, AQL 0,65 / 2,5 | **ASME B16.9**, **ASTM A403**, ASTM A967, ISO 12944-2, ISO 9223. ⚠ SS304 rentan pitting di air laut → sarankan 316/316L. Berat 510 – 530 g. OD 60,0 – 60,6 mm (±0,3). Kritis 100% (n ≥ lot) · Mayor **F** n=20 Ac0/Re1 · Minor **F** n=20 Ac1/Re2. |

**Cek tambahan:** **Simpan** → muncul di daftar · **Unduh PDF** (5 bagian + kolom pengesahan) · **Kalkulator disposisi** (pilih "Flash / sirip", centang semua syarat → *REWORK / FINISHING DIIZINKAN*; hilangkan satu centang → *TOLAK*) · **Buat dataset SPC** → LSL/USL berat otomatis terisi.
