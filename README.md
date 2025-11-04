# 📰 Topic Modeling Judul Berita Indonesia
<p align="center">
   <a href="#"><img src="https://img.shields.io/badge/Jupyter%20Notebook-%23F37626?style=for-the-badge&logo=jupyter&logoColor=white" alt="Jupyter Notebook" /></a>
   <a href="#"><img src="https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python" /></a>
   <a href="#"><img src="https://img.shields.io/badge/scikit--learn-1.x-F7931E?style=for-the-badge&logo=scikitlearn&logoColor=white" alt="scikit-learn" /></a>
   <a href="#"><img src="https://img.shields.io/badge/pandas-1.x-150458?style=for-the-badge&logo=pandas&logoColor=white" alt="pandas" /></a>
   <a href="#"><img src="https://img.shields.io/badge/NumPy-1.x-013243?style=for-the-badge&logo=numpy&logoColor=white" alt="NumPy" /></a>
   <a href="#"><img src="https://img.shields.io/badge/Matplotlib-11557C?style=for-the-badge&logo=matplotlib&logoColor=white" alt="Matplotlib" /></a>
   <a href="#"><img src="https://img.shields.io/badge/Seaborn-4C9BD6?style=for-the-badge" alt="Seaborn" /></a>
   <a href="#"><img src="https://img.shields.io/badge/NLTK-85C1E9?style=for-the-badge" alt="NLTK" /></a>
   <a href="#"><img src="https://img.shields.io/badge/Sastrawi-28A745?style=for-the-badge" alt="Sastrawi" /></a>
   <a href="#"><img src="https://img.shields.io/badge/WordCloud-2C3E50?style=for-the-badge" alt="WordCloud" /></a>
   <a href="#"><img src="https://img.shields.io/badge/re%20(regex)-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="re (regex)" /></a>
</p>

Proyek ini mengeksplorasi topik-topik tersembunyi pada judul berita berbahasa Indonesia menggunakan teknik Topic Modeling. Kami memproses teks (normalisasi, tokenisasi, stopword removal, stemming, lemitization), mengubahnya menjadi representasi numerik (TF‑IDF), lalu mengekstrak topik menggunakan Latent Dirichlet Allocation (LDA). Hasilnya divisualisasikan dalam tabel kata kunci, bar chart, word cloud per topik, serta proyeksi t‑SNE.

## ✨ Ringkasan

- Dataset: `dataset/indonesian-news-title.csv` (berisi kolom `date`, `url`, `title`, dan `category`.)
- Pemrosesan Teks: normalisasi (lowercase, hapus angka & tanda baca), tokenisasi NLTK, stopword Bahasa Indonesia (Sastrawi + daftar kustom), stemming (Sastrawi)
- Vektorisasi: TF‑IDF (`max_df=0.95`, `min_df=2`, `max_features=1000`)
- Model: LDA (scikit‑learn) dengan `NUM_TOPICS=10`, `learning_method='online'`, `random_state=42`
- Visualisasi: distribusi kategori, word cloud keseluruhan, tabel kata teratas per topik, bar chart kata teratas per topik, word cloud per topik, t‑SNE (setelah reduksi dimensi dengan TruncatedSVD)
- Performa: secara default memproses sampel `500` baris untuk mempercepat (stemming Sastrawi relatif lambat); bisa dinaikkan sesuai kebutuhan

## 📂 Struktur Repository

```
Topic-Modeling-Project/
├─ Kelompok_2_TM.ipynb          # Notebook utama analisis & modeling
├─ dataset/
│  └─ indonesian-news-title.csv # Dataset judul berita Indonesia
└─ README.md                    # Dokumentasi proyek ini
```

## 🧭 Alur Pengerjaan

1. Data Understanding

   - Memuat `./dataset/indonesian-news-title.csv`
   - Cek jumlah baris, panjang judul, duplikasi judul, nilai kosong
   - (Opsional) Visualisasi distribusi kategori dan word cloud keseluruhan

2. Text Processing

   - Normalisasi: lowercase, hapus angka dan tanda baca, trim spasi
   - Tokenisasi: `nltk.word_tokenize`
   - Stopword Removal: Sastrawi + daftar stopword kustom (mis. `yg`, `dg`, `rt`, `ke`, `di`, `rp`, dll.)
   - Stemming: Sastrawi (`StemmerFactory`)
   - Catatan: stemming paling lambat; gunakan sampling data untuk eksperimen cepat

3. Vektorisasi

   - TF‑IDF: `TfidfVectorizer(max_df=0.95, min_df=2, max_features=1000)`

4. Topic Modeling (LDA)

   - Model: `LatentDirichletAllocation(n_components=NUM_TOPICS, learning_method='online', random_state=42)`
   - Default `NUM_TOPICS = 10` (silakan sesuaikan)

5. Visualisasi Hasil
   - Tabel kata teratas per topik (Top‑N words)
   - Bar chart kata teratas per topik
   - Word cloud per topik (hingga 6 topik pertama secara default)
   - t‑SNE 2D (setelah reduksi dimensi dengan `TruncatedSVD(n_components=50)`), diwarnai berdasarkan `category` bila tersedia

## 🚀 Cara Menjalankan (Windows/PowerShell)

Disarankan membuat virtual environment agar dependensi terisolasi.

Langkah cepat:

1.  **Clone repositori:**
    ```bash
    git clone https://github.com/zeniramadan/Topic-Modeling-Project.git
    ```

2.  **Install dependensi:**

    Karena proyek ini menggunakan Jupyter Notebook dan *library* Python, Anda perlu menginstal dependensi yang diperlukan.  Asumsikan kebutuhan `pip`:

    ```powershell
    pip install jupyter pandas numpy scikit-learn nltk Sastrawi matplotlib seaborn wordcloud re
    ```

    Pastikan Anda memiliki Python dan pip terinstal. Jika belum, Anda dapat mengunduhnya dari [https://www.python.org/](https://www.python.org/).  Anda mungkin perlu menginstal NLTK data juga:
        ```python
        import nltk
        nltk.download('stopwords')
        nltk.download('punkt')
        ```

3. **Jalankan proyek:**

    Buka *notebook* Jupyter atau VSCode:

    ```bash
    Kelompok_2_TM.ipynb
    ```

    Kemudian, jalankan sel-sel dalam *notebook* untuk menjalankan analisis *topic modeling*.

Lalu jalankan sel dari atas ke bawah di `Kelompok_2_TM.ipynb`. Pastikan `file_path` di notebook menunjuk ke `./dataset/indonesian-news-title.csv`.

## ⚙️ Konfigurasi yang Mudah Disesuaikan

- Ukuran sampel: ubah jumlah baris yang diambil (default 500) untuk trade‑off kecepatan vs akurasi
- Jumlah topik: ganti nilai `NUM_TOPICS` (mis. 5, 10, 15, …)
- Parameter TF‑IDF: sesuaikan `max_df`, `min_df`, dan `max_features`
- Stopwords kustom: tambah/kurangi kata pada daftar stopword sesuai domain
- Reproducibility: semua langkah kunci menggunakan `random_state=42`

## 🧰 Tech Stack

- Bahasa & Runtime: Python 3.10+ 🐍
- Data & Numerik: pandas, NumPy 📊
- NLP: NLTK, Sastrawi 🔤
- Fitur & Model: scikit-learn (TF‑IDF, LDA, TruncatedSVD, TSNE) 🤖
- Visualisasi: Matplotlib, Seaborn, WordCloud 📈
- Utilitas Teks: re (regex) 🧩
- Notebook: Jupyter 📓

## 📝 Catatan & Tips

- Stemming Sastrawi cukup lambat pada dataset besar; gunakan sampling saat eksplorasi awal
- Untuk LDA, `CountVectorizer` sering kali cocok; di proyek ini digunakan TF‑IDF dan tetap bekerja baik
- Jika memori terbatas, hindari `toarray()` pada matriks sparse (gunakan pipeline SVD → t‑SNE seperti di notebook)


## 👥 Project Team 2
- 10222017 Zeni Ramadan
- 10222000 Ai Hamidah
- 10222000 Abdul Ropi
