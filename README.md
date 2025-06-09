# Analisis Siklus Hidup Pelanggan dan Prediksi Churn Menggunakan Rantai Markov Waktu Diskrit

Repositori ini berisi kode dan data untuk proyek akhir mata kuliah Proses Stokastik, yang mengimplementasikan model Rantai Markov Waktu Diskrit (DTMC) untuk menganalisis dan memprediksi *customer churn* pada industri telekomunikasi.

## Deskripsi Proyek

Penelitian ini bertujuan untuk memodelkan perjalanan pelanggan melalui berbagai fase loyalitas (`New`, `Established`, `Loyal`) hingga `Churn`. Dengan menggunakan pendekatan DTMC, kami mengestimasi probabilitas transisi bulanan antar status untuk mengidentifikasi fase paling kritis dan memprediksi perilaku pelanggan jangka panjang.

## Struktur Repository

```
.
├── data/
│   └── Telco-Customer-Churn.csv  (Dataset mentah)
├── notebooks/
│   └── analisis_churn.ipynb      (Kode utama analisis dalam Jupyter Notebook)
├── output/
│   └── (Folder untuk menyimpan plot dan hasil)
├── .gitignore
├── LICENSE
├── README.md
└── requirements.txt            (Daftar pustaka Python yang dibutuhkan)
```

## Cara Reproduksi Hasil

Untuk menjalankan analisis ini di mesin lokal Anda, ikuti langkah-langkah berikut:

1.  **Clone repositori ini:**
    ```bash
    git clone [https://github.com/zakizulham/proyek-stokastik-churn-telekomunikasi](https://github.com/zakizulham/proyek-stokastik-churn-telekomunikasi)
    cd proyek-stokastik-churn-telekomunikasi
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
    ```bash
    pip install -r requirements.txt
    ```

4.  **Jalankan Jupyter Notebook:**
    Buka dan jalankan semua sel di dalam `notebooks/analisis_churn.ipynb`.
    ```bash
    jupyter notebook notebooks/analisis_churn.ipynb
    ```

## Hasil Utama

Analisis menunjukkan bahwa pelanggan pada fase **`New` (1-12 bulan)** memiliki risiko churn bulanan tertinggi secara signifikan. Model DTMC memprediksi bahwa pelanggan baru memiliki probabilitas kumulatif untuk churn yang tinggi dalam 1-2 tahun pertama, yang menekankan pentingnya strategi retensi yang tertarget pada fase awal siklus hidup pelanggan.

## Lisensi

Proyek ini dilisensikan di bawah Lisensi MIT. Lihat file `LICENSE` untuk detail lebih lanjut.