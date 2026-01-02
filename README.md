# Pemodelan Topik "Indonesia Gelap" pada Media Berita: Pendekatan Hybrid Word2Vec & BERTopic

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![NLP](https://img.shields.io/badge/NLP-Topic%20Modeling-green)
![Library](https://img.shields.io/badge/GenSim-Word2Vec-yellow)
![Library](https://img.shields.io/badge/BERTopic-c--TF--IDF-orange)

## 📌 Ringkasan Eksekutif

Repositori ini mendokumentasikan riset NLP mengenai fenomena viral **"Indonesia Gelap"** (Februari 2025). Riset ini bertujuan membedah bagaimana portal berita arus utama (*mainstream media*) membingkai isu yang bermula sebagai kritik sosial di media sosial ini.

Alih-alih menggunakan model bahasa standar (seperti BERT multilingual), proyek ini mengimplementasikan pendekatan **Hybrid Topic Modeling** dengan mengintegrasikan **Custom Word2Vec (CBOW)** ke dalam arsitektur **BERTopic**. Pendekatan ini dipilih untuk menangkap nuansa semantik lokal dan bahasa gaul (*slang*) yang spesifik pada wacana politik Indonesia.

## 👤 Penulis & Kontributor

**Pemilik Repositori (Dokumentasi Portofolio):**
* **Nur’aini** - http://www.linkedin.com/in/nuraiinii01 | Nuraiinii1001@gmail.com
*(Program Studi Statistika dan Sains Data, IPB University)*

---
**Tim Riset (Kelompok 3):**
Proyek ini dikembangkan secara kolaboratif sebagai bagian dari tugas akademik di IPB University oleh:
* **Nur’aini**
* Nabila Fida Millati
* Reyuli Andespa

**Dosen Pembimbing:**
* Cici Suhaeni
* Bagus Sartono
* Gerry Alfa Dito

## 📖 Konteks Masalah

Istilah **"Indonesia Gelap"** muncul sebagai tagar perlawanan digital yang menyimbolkan "kegelapan" tata kelola negara akibat:
1.  **Tekanan Ekonomi:** Kelangkaan LPG 3kg, kenaikan PPN, dan harga bahan pokok.
2.  **Isu Kebijakan:** Kontroversi program "Makan Bergizi Gratis".
3.  **Kesejahteraan:** Penundaan insentif akademik dan guru honorer.

**Rumusan Masalah:**
Apakah media berita memperkuat kritik publik ini, atau justru "membajak" istilah tersebut untuk membingkai isu lain (seperti kriminalitas murni) demi *clickbait*?

## 📂 Spesifikasi Data

* **Sumber Data:** 5 Portal Berita Nasional (CNN Indonesia, Detik, Kompas, Tempo, Tribun News).
* **Kata Kunci:** "Indonesia Gelap".
* **Periode:** 1 – 22 Februari 2025.
* **Volume:** 352 Artikel (Pasca-cleaning).

## 🛠️ Metodologi (Pipeline Teknis)

Kami merancang alur kerja *end-to-end* sebagai berikut:

1.  **Data Acquisition:** *Web Scraping* menggunakan Python.
2.  **Advanced Preprocessing:** Pembersihan regex, normalisasi teks, *stopword removal* (Sastrawi), dan *stemming*.
3.  **Feature Extraction (Novelty):**
    * Melatih model **Word2Vec (CBOW)** dari nol (*scratch*) menggunakan korpus berita terkumpul.
    * Tujuan: Menangkap kedekatan semantik kata unik seperti *"subsidi"* dengan *"gas melon"* yang mungkin tidak tertangkap model pre-trained global.
4.  **Dimensionality Reduction:** UMAP (*Uniform Manifold Approximation and Projection*).
5.  **Clustering:** HDBSCAN untuk deteksi klaster padat.
6.  **Topic Representation:** Menggunakan **c-TF-IDF** untuk pembobotan kata kunci per topik.
7.  **Evaluasi:** Optimasi parameter berdasarkan **Coherence Score ($C_v$)**.

## 📊 Hasil & Temuan Utama

Model terbaik menghasilkan **Coherence Score ($C_v$) 0.6277** dengan 4 topik dominan:

| Topik ID | Label Tema | Kata Kunci Dominan | Interpretasi |
| :--- | :--- | :--- | :--- |
| **0** | **Tragedi & Kriminalitas** | `kebakaran`, `polisi`, `korban`, `tewas`, `rumah` | Penggunaan kata "Gelap" secara harfiah. Berita kebakaran, pembunuhan, dan pencurian yang dilabeli dengan tagar viral. |
| **1** | **Kritik Sosial-Politik** | `makan`, `program`, `anggaran`, `ppn`, `subsidi` | **Representasi Suara Publik:** Topik ini selaras dengan intensi asli netizen, membahas beban hidup dan kebijakan pemerintah. |
| **2** | **Kecelakaan & Bencana** | `truk`, `tabrak`, `jalan`, `bencana`, `hujan` | Berita kecelakaan lalu lintas dan bencana alam (banjir/longsor). |
| **3** | **Kekerasan Seksual** | `perkosa`, `perempuan`, `seksual`, `tahan` | Kasus kejahatan asusila. Media membingkai ini sebagai "sisi gelap" moralitas masyarakat. |

## 💡 Analisis Mendalam (Insights)

### 1. Pergeseran Makna (Semantic Drift)
Terjadi divergensi tajam antara diskursus publik dan media:
* **Publik (Netizen):** Menggunakan "Indonesia Gelap" 100% sebagai **metafora politik**.
* **Media Berita:** Hanya sekitar 25% (Topik 1) yang membahas politik. Selebihnya (75%) menggunakan istilah ini untuk berita kriminal, kecelakaan, dan bencana.

### 2. Strategi "News Jacking"
Data menunjukkan indikasi kuat bahwa media melakukan *news jacking* (pembajakan isu). Portal berita menyematkan kata kunci viral "Indonesia Gelap" pada berita kriminal umum (Topik 0 & 3) yang sebenarnya tidak berhubungan dengan kritik kebijakan negara, kemungkinan besar untuk meningkatkan trafik pembaca (*engagement*).

### 3. Keunggulan Word2Vec vs BERT Multilingual
Pada eksperimen ini, Word2Vec (CBOW) terbukti lebih unggul dalam membentuk topik yang koheren dibandingkan BERT Multilingual. Hal ini karena dataset bersifat sangat lokal dan spesifik, sehingga *embedding* yang dilatih sendiri mampu menangkap konteks mikro jauh lebih baik daripada model bahasa besar yang dilatih pada korpus global.

## 🚀 Cara Menjalankan Kode

1.  **Clone Repositori:**
    ```bash
    git clone [https://github.com/username-anda/indonesia-gelap-topic-modeling.git](https://github.com/username-anda/indonesia-gelap-topic-modeling.git)
    ```
2.  **Instalasi Dependensi:**
    ```bash
    pip install -r requirements.txt
    ```
    *(Pastikan library `bertopic`, `gensim`, `sastrawi`, dan `scikit-learn` terinstall)*

3.  **Eksekusi Notebook:**
    Jalankan file `Topic_Modeling_Analysis.ipynb` melalui Jupyter Notebook atau Google Colab.

## 📚 Referensi

* Grootendorst, M. (2022). *BERTopic: Neural topic modeling with a class-based TF-IDF procedure*.
* Mikolov, T., et al. (2013). *Efficient Estimation of Word Representations in Vector Space*.
* (Referensi lengkap tersedia di dalam dokumen laporan).

---
*Disclaimer: Repositori ini disusun sebagai arsip dokumentasi pribadi dan portofolio data science Nur'aini, berdasarkan hasil riset kelompok yang dilakukan di IPB University.*
