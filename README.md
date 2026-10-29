# Prediksi Kelayakan Minum (Potabilitas) Air Berdasarkan Indikator Parameter Kimiawi Air

Proyek UTS **Data Science** — Program Studi Informatika, Jurusan Informatika, Fakultas Teknik Industri,
Universitas Pembangunan Nasional "Veteran" Yogyakarta. Tahun Ajaran 2026/2027 (Semester Ganjil).
Dosen pengampu: **Dhimas Arief Dharmawan**.

## Kelompok

- **Nomor kelompok:** _(isi nomor kelompok)_
- **Nama kelompok:** Datadoom

| No | Nama | NIM |
|---|---|---|
| 1 | Mahendra Rajwaa Putra Pamungkas | 123240039 |
| 2 | Muhammad Athalla Bagaskara | 123240212 |
| 3 | Ryan Haqqi Prarista | 123240067 |
| 4 | Muhammad Ridho Hikmatul Maulana | 123240218 |

## Ringkasan

Penelitian ini merancang klasifikasi biner (layak = 1, tidak layak = 0) untuk memprediksi potabilitas air
dari sembilan parameter fisik dan kimia, mengikuti kerangka CRISP-DM. Model kandidat yang direncanakan:
Random Forest dan XGBoost. Hasil prediksi diposisikan sebagai alat bantu penapisan awal, bukan pengganti
uji laboratorium.

**Cakupan pengumpulan UTS:** Business Understanding dan Data Understanding.
Fase Data Preparation, Modeling, Evaluation, dan Deployment masih berupa rencana (belum ada eksperimen).

## Struktur Repositori

```
.
├── README.md
├── laporan/
│   └── Laporan_UTS_Data_Science_Datadoom.docx
├── data/
│   └── water_potability.csv
├── src/
│   └── analisis_eda.py
└── hasil/
    ├── hasil_analisis.json
    └── fig/            # f1_kelas, f2_missing, f3_histogram, f4_boxplot_target, f5_korelasi, f6_korelasi_target
```

## Dataset

- Sumber: Kaggle, [Water Quality / Water Potability](https://www.kaggle.com/datasets/adityakadiwal/water-potability) (Aditya Kadiwal)
- File: `water_potability.csv` — 3.276 baris, 10 kolom (9 fitur numerik + target `Potability`)
- Fitur: `ph`, `Hardness`, `Solids`, `Chloramines`, `Sulfate`, `Conductivity`, `Organic_carbon`, `Trihalomethanes`, `Turbidity`
- Nilai kosong: `ph` 14,99%, `Sulfate` 23,84%, `Trihalomethanes` 4,95%; tidak ada baris duplikat
- Kelas: 60,99% tidak layak, 39,01% layak
- Lisensi: mengikuti ketentuan pada halaman Kaggle. Atribusi kepada pemilik dataset wajib dicantumkan.

## Cara Menjalankan Ulang

Prasyarat: Python 3.12 dengan `pandas`, `scipy`, `matplotlib`, `seaborn`
(versi saat analisis: pandas 3.0.2, SciPy 1.17.1, matplotlib 3.10.8, seaborn 0.13.2).

```bash
pip install pandas scipy matplotlib seaborn
python src/analisis_eda.py data/water_potability.csv hasil
```

Skrip menghitung seluruh statistik pada laporan, menyimpan `hasil/hasil_analisis.json`,
dan menghasilkan enam grafik di `hasil/fig/`. Dataset asli tidak diubah.

## Temuan Utama Data Understanding

- Korelasi tiap fitur dengan target sangat lemah (−0,030 sampai 0,034); tidak ada fitur yang berbeda signifikan antarkelas (Mann–Whitney U).
- Korelasi antarfitur rendah (|r| maksimum 0,172), sehingga multikolinearitas bukan masalah.
- Hanya 2.011 dari 3.276 baris yang lengkap.
- Pembanding minimum: akurasi prediksi kelas mayoritas 60,99%.

## Batasan

Dataset tidak memuat parameter mikrobiologis maupun logam berat, dan asal-usul data serta cara pelabelan
tidak terdokumentasi. Model tidak menggantikan uji laboratorium maupun standar kualitas air yang berlaku.
