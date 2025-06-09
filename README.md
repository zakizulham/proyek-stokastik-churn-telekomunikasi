# Analisis Siklus Hidup Pelanggan dan Prediksi Churn Menggunakan Rantai Markov Waktu Diskrit

[![Python 3.13](https://img.shields.io/badge/python-3.13-blue.svg)](https://www.python.org/downloads/release/python-3130/)
[![Maintenance](https://img.shields.io/badge/Maintained%3F-no-red.svg)](https://github.com/stevenrhart/predicting-claims/graphs/commit-activity)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Repositori ini berisi kode dan data untuk proyek akhir mata kuliah Proses Stokastik, yang mengimplementasikan model Rantai Markov Waktu Diskrit (DTMC) untuk menganalisis dan memprediksi *customer churn* pada industri telekomunikasi.

**[Deskripsi](#Deskripsi)** | **[Struktur Repository](#Struktur)** | **[Reproduksi Hasil](#Reproduksi)** | **[Ringkasan Proyek](#Ringkasan)** | **[Lisensi](#Lisensi)** 

lihat [laporan lengkap](https://github.com/zakizulham/proyek-stokastik-churn-telekomunikasi/blob/main/laporan/analisis_churn.pdf)

## Deskripsi Proyek <a id='Deskripsi'></a>

Penelitian ini bertujuan untuk memodelkan perjalanan pelanggan melalui berbagai fase loyalitas (`New`, `Established`, `Loyal`) hingga `Churn`. Dengan menggunakan pendekatan DTMC, kami mengestimasi probabilitas transisi bulanan antar status untuk mengidentifikasi fase paling kritis dan memprediksi perilaku pelanggan jangka panjang.

## Struktur Repository <a id='Struktur'></a>

```
.
├── data/
│   └── Telco-Customer-Churn.csv
├── laporan/
│   ├── analisis_churn.pdf
│   ├── main.tex
│   └── references.bib
├── notebooks/
│   └── analisis_churn.ipynb      
├── output/
│   └── plot_distribusi_status.png
├── .gitignore
├── LICENSE
├── README.md
└── requirements.txt
```

## Cara Reproduksi Hasil <a id='Reproduksi'></a>

Untuk menjalankan analisis ini di mesin lokal Anda, ikuti langkah-langkah berikut:

1.  **Clone repositori ini:**
    ```bash
    git clone https://github.com/zakizulham/proyek-stokastik-churn-telekomunikasi.git && cd proyek-stokastik-churn-telekomunikasi
    ```

2.  **Buat dan aktifkan Virtual Environment (Direkomendasikan):**
    ```bash
    # Membuat environment
    python -m venv venv

    # Mengaktifkan di Windows
    .\venv\Scripts\activate

    # Mengaktifkan di MacOS/Linux
    source venv/bin/activate
    ```

3.  **Instal pustaka yang dibutuhkan:**

    Menggunakan Python 3.13.2

    Pustaka yang dibutuhkan:

    ```bash
    pip install -r requirements.txt
    ```

4.  **Jalankan Jupyter Notebook:**

    Buka dan jalankan semua sel di dalam `notebooks/analisis_churn.ipynb`.
    ```bash
    jupyter notebook notebooks/analisis_churn.ipynb
    ```

## Ringkasan Proyek <a id='Ringkasan'></a>

**[Executive Summary](#exec-summary)** | **[Datasets](#data)** | **[Wrangling](#wrangling)** | **[EDA](#eda)** | **[Results](#results)** | **[Future](#future)**

### Executive Summary <a id='exec-summary'></a>
Penelitian ini mengimplementasikan model Rantai Markov Waktu Diskrit (DTMC) untuk menganalisis masalah krusial dalam industri telekomunikasi: *customer churn*. Berbeda dengan pendekatan klasifikasi biner, model ini memetakan perjalanan pelanggan melalui tiga fase siklus hidup (`New`, `Established`, `Loyal`) untuk memahami *kapan* dan *mengapa* churn terjadi. Hasil utama menunjukkan fenomena churn yang sangat terkonsentrasi pada fase awal, di mana pelanggan baru memiliki probabilitas yang sangat tinggi untuk berhenti dalam beberapa bulan pertama. Temuan ini mengimplikasikan bahwa strategi retensi yang efektif harus bersifat proaktif, sangat dini, dan tertarget pada segmen pelanggan baru.

### Dataset <a id='data'></a>
* **Sumber:** [Telco Customer Churn](https://www.kaggle.com/datasets/blastchar/telco-customer-churn) oleh Blastchar di Kaggle.
* **Deskripsi:** Dataset ini berisi 7.043 observasi pelanggan dengan 21 atribut, mencakup informasi demografis, detail layanan yang digunakan (telepon, internet, TV), jenis kontrak, dan status `Churn`.
* **Variabel Kunci:** `tenure` (masa berlangganan dalam bulan) dan `Churn` (status berhenti berlangganan) menjadi variabel utama yang digunakan untuk membangun model DTMC.

### Wrangling (Pemrosesan Data) <a id='wrangling'></a>
Proses persiapan data difokuskan untuk mentransformasi data mentah menjadi format yang sesuai untuk pemodelan DTMC. Langkah utamanya adalah rekayasa fitur pada variabel `tenure` untuk menciptakan kolom kategorikal `TenureGroup`. Pelanggan dikelompokkan ke dalam tiga status transient berdasarkan masa berlangganan mereka: `New` (1-12 bulan), `Established` (13-48 bulan), dan `Loyal` (>48 bulan). Status `Churn` menjadi status penyerap (absorbing state) dalam model.

### EDA (Analisis Data Eksploratif) <a id='eda'></a>
Analisis eksploratif awal menunjukkan adanya hubungan yang kuat antara `tenure` dan kecenderungan `Churn`. Visualisasi sederhana pada data mentah mengonfirmasi bahwa jumlah pelanggan yang churn paling banyak terkonsentrasi pada kelompok dengan `tenure` rendah. Observasi ini menjadi justifikasi utama untuk tidak menggunakan model churn yang seragam, melainkan memilih pendekatan berbasis siklus hidup yang dapat menangkap dinamika yang bergantung pada waktu ini.

### Results (Hasil) <a id='results'></a>
Hasil pemodelan DTMC memberikan wawasan yang tajam dan kuantitatif:
1.  **Risiko Churn Terkonsentrasi:** Model membuktikan bahwa risiko churn tidak merata. Pelanggan di fase `New` menunjukkan probabilitas churn bulanan yang sangat tinggi, yang menyebabkan eksodus pelanggan secara masif pada bulan-bulan pertama.
2.  **Kegagalan "Kelulusan":** Probabilitas seorang pelanggan baru untuk berhasil transisi dan bertahan hingga mencapai fase `Established` atau `Loyal` sangatlah kecil. Sebagian besar perjalanan pelanggan berakhir di status `Churn` sebelum sempat menjadi tetap.
3.  **Konvergensi Cepat:** Sistem dengan cepat bergerak menuju state `Churn`. Ini menegaskan bahwa bagi sebagian besar pelanggan baru, churn adalah peristiwa jangka pendek, bukan hasil dari ketidakpuasan yang terakumulasi dalam jangka panjang.

### Future (Pengembangan Selanjutnya) <a id='future'></a>
Untuk meningkatkan akurasi dan kedalaman analisis, beberapa arah pengembangan di masa depan dapat dieksplorasi:
* **Status yang Lebih Granular:** Menggabungkan `tenure` dengan variabel lain seperti `Contract` (jenis kontrak) untuk menciptakan status yang lebih spesifik (misalnya, `New-MonthlyContract` vs `New-YearlyContract`).
* **Model Stokastik Lanjutan:** Mengimplementasikan Rantai Markov non-homogen yang memungkinkan probabilitas transisi berubah seiring waktu, atau model regresi berbasis Markov untuk memasukkan lebih banyak variabel prediktor.
* **Validasi Data Panel:** Menguji dan memvalidasi model ini menggunakan data panel (longitudinal) untuk mengamati transisi pelanggan secara langsung dan membandingkannya dengan hasil estimasi dari data *cross-sectional*.

## Lisensi <a id='Lisensi'></a>

Proyek ini dilisensikan di bawah Lisensi MIT. Lihat file `LICENSE` untuk detail lebih lanjut.
