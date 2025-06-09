# Analisis Siklus Hidup Pelanggan dan Prediksi Churn Menggunakan Rantai Markov Waktu Diskrit

Repositori ini berisi kode dan data untuk proyek akhir mata kuliah Proses Stokastik, yang mengimplementasikan model Rantai Markov Waktu Diskrit (DTMC) untuk menganalisis dan memprediksi *customer churn* pada industri telekomunikasi.

## Deskripsi Proyek

Penelitian ini bertujuan untuk memodelkan perjalanan pelanggan melalui berbagai fase loyalitas (`New`, `Established`, `Loyal`) hingga `Churn`. Dengan menggunakan pendekatan DTMC, kami mengestimasi probabilitas transisi bulanan antar status untuk mengidentifikasi fase paling kritis dan memprediksi perilaku pelanggan jangka panjang.

## Struktur Repository

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

## Cara Reproduksi Hasil

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

## Hasil Utama

Analisis dari model DTMC mengungkapkan sebuah fenomena churn yang **sangat dominan dan terjadi dengan cepat** pada pelanggan di fase **`New` (1-12 bulan)**. Berbeda dengan pandangan umum tentang churn yang terjadi secara bertahap, model ini memprediksi bahwa eksodus pelanggan terjadi secara masif **dalam beberapa bulan pertama saja**.

Temuan krusial lainnya adalah probabilitas seorang pelanggan baru untuk berhasil "lulus" ke fase `Established` atau `Loyal` sangatlah kecil. Model menunjukkan bahwa hampir semua pelanggan baru dihadapkan pada dua takdir dalam jangka pendek: churn, atau dengan probabilitas yang jauh lebih kecil, tetap berjuang di fase awal. Hal ini mengimplikasikan bahwa jendela kesempatan untuk melakukan retensi sangatlah sempit, dan intervensi harus dilakukan secara **agresif dan sangat dini** dalam siklus hidup pelanggan untuk dapat memberikan dampak yang berarti.

## Lisensi

Proyek ini dilisensikan di bawah Lisensi MIT. Lihat file `LICENSE` untuk detail lebih lanjut.