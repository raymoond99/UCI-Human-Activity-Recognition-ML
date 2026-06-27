# Human Activity Recognition (UCI HAR) Using Machine Learning

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Proyek Machine Learning untuk memprediksi 6 jenis aktivitas fisik manusia (dinamis dan statis) berdasarkan data sensor *accelerometer* dan *gyroscope* dari *smartphone* menggunakan berbagai algoritma klasifikasi.

## Angka Kelompok

| Nama Lengkap | NIM | Program Studi |
| :--- | :--- | :--- |
| **Raymundus Ariel Abas** | `103132430021` | S-1 Sains Data |
| **Keyla Azzahra** | `103132400017` | S-1 Sains Data |

---

## Latar Belakang

**Permasalahan** Pengenalan aktivitas manusia (*Human Activity Recognition*) sangat krusial dalam pengembangan teknologi *smart healthcare*, pemantauan kebugaran, dan *Ambient Assisted Living* (AAL). Mendeteksi aktivitas secara akurat dari data sensor mentah membutuhkan ekstraksi fitur yang kompleks dan model klasifikasi yang tangguh.

**Tujuan** Mengembangkan model Machine Learning yang mampu mengklasifikasikan 6 aktivitas dasar manusia (Berjalan, Berjalan ke Atas, Berjalan ke Bawah, Duduk, Berdiri, dan Berbaring) berdasarkan 561 fitur yang diekstrak dari sinyal sensor *smartphone*.

**Tantangan** * **High Dimensionality:** Dataset memiliki dimensi yang sangat tinggi (561 fitur numerik).
* **Feature Overlap:** Aktivitas statis seperti "Duduk" dan "Berdiri" seringkali memiliki pola sinyal sensor yang sangat mirip, sehingga rentan terjadi kesalahan klasifikasi (*misclassification*).

---

## Dataset

* **Sumber:** UCI Machine Learning Repository — Human Activity Recognition Using Smartphones Dataset
* **Statistik Dataset:**

| Metrik | Jumlah / Keterangan |
| :--- | :--- |
| **Jumlah Data Latih (Train)** | 7,352 records |
| **Jumlah Data Uji (Test)** | 2,947 records |
| **Jumlah Fitur** | 561 fitur numerik (Time & Frequency domain) |
| **Target Variable** | `Activity` (6 Kelas Kategorikal) |

* **Deskripsi Kelas Target:**
  1. `WALKING`
  2. `WALKING_UPSTAIRS`
  3. `WALKING_DOWNSTAIRS`
  4. `SITTING`
  5. `STANDING`
  6. `LAYING`

---

## Metodologi

### 1. Exploratory Data Analysis (EDA)
* Analisis distribusi target variable untuk memastikan dataset seimbang (*balanced*).
* Inspeksi kelengkapan data (*missing values check*).

### 2. Data Preprocessing
* **Data Cleaning:** Menghapus fitur yang tidak relevan (jika ada).
* **Encoding:** Menggunakan `LabelEncoder` untuk mengubah target kelas kategorikal (teks aktivitas) menjadi representasi numerik (0-5).
* Fitur numerik tidak dilakukan *scaling* ulang karena dataset bawaan UCI HAR sudah di-normalisasi pada rentang [-1, 1].

### 3. Model Machine Learning
Diimplementasikan 4 model yang dibagi menjadi tipe *Baseline* dan *Advanced Ensemble*:

| Kategori | Model | Deskripsi |
| :--- | :--- | :--- |
| **Baseline** | K-Nearest Neighbors (KNN) | Instance-based learning berdasarkan jarak terdekat. |
| **Baseline** | Support Vector Machine (SVM) | Klasifikasi berbasis hyperplane optimal dengan kernel RBF. |
| **Ensemble** | Random Forest | Ensemble method berbasis decision tree. |
| **Ensemble** | XGBoost | Gradient boosting yang powerful dan efisien. |

### 4. Evaluasi
* **Metrik:** Accuracy.
* **Visualisasi:** Model Comparison Bar Chart & Confusion Matrix.

---

## Struktur Repository

```text
TUBES ML (2)/
│
├── data/
│   ├── test.csv                             # Dataset uji mentah
│   ├── test_clean.csv                       # Data uji siap pakai (hasil preprocessing)
│   ├── train.csv                            # Dataset latih mentah
│   └── train_clean.csv                      # Data latih siap pakai (hasil preprocessing)
│
├── Figures/
│   ├── 01_model_comparison.png              # Visualisasi perbandingan akurasi
│   └── 02_confusion_matrix.png              # Confusion matrix dari model terbaik
│
├── models/
│   ├── Best_Model_SVM.pkl                   # Model terbaik siap deploy
│   ├── knearest_neighbors_baseline.pkl      # Model KNN tersimpan
│   ├── random_forest_advanced_ensemble.pkl  # Model Random Forest tersimpan
│   └── xgboost_advanced_ensemble.pkl        # Model XGBoost tersimpan
│
├── notebooks/
│   ├── 01_EDA_And_Preprocessing.ipynb       # Proses cleaning, label encoding & EDA
│   └── 02_Model_Training_and_Evaluation.ipynb # Pipeline training & evaluasi model
│
├── requirements.txt                         # Dependencies proyek
└── README.md                                # Dokumentasi (file ini)
💻 Instalasi & PenggunaanPrerequisitesPython 3.8 atau lebih barupip (Python package manager)Langkah InstalasiClone repositoryBashgit clone [https://github.com/](https://github.com/)[USERNAME_GITHUB_KAMU]/[NAMA_REPO_KAMU].git
cd [NAMA_REPO_KAMU]
Install dependenciesBashpip install -r requirements.txt
(Catatan: Pengguna Windows dapat menggunakan py -m pip install -r requirements.txt)Cara Menjalankan PipelineProyek ini menggunakan arsitektur interaktif berbasis Jupyter Notebook.Buka folder proyek di VS Code atau Jupyter Lab.Jalankan notebooks/01_EDA_And_Preprocessing.ipynb dengan menekan tombol Run All. Skrip ini akan memuat dataset, melakukan inspeksi awal, dan menerapkan encoding.Jalankan notebooks/02_Model_Training_and_Evaluation.ipynb dengan menekan tombol Run All. Skrip ini akan melatih ke-4 model ML, menghasilkan metrik evaluasi, mencetak visualisasi ke layar (serta menyimpannya jika diatur), dan mengekspor model ke folder models/.🏆 Hasil & AnalisisPerforma ModelEvaluasi pada data uji (test set) menghasilkan urutan performa sebagai berikut:Support Vector Machine (SVM) — 95.05% 🏆XGBoost Classifier — 93.79% 🥈Random Forest Classifier — 92.60% 🥉K-Nearest Neighbors (KNN) — 90.02%KesimpulanModel Support Vector Machine (SVM) dengan kernel RBF terbukti menjadi model yang paling optimal untuk dataset UCI HAR. SVM mampu menangani ruang dimensi tinggi (561 fitur) dengan sangat baik dalam memisahkan batas keputusan kelas aktivitas dinamis dan statis tanpa mengalami kendala overfitting yang berlebihan.🛠️ TeknologiTeknologiKegunaanPython 3.xBahasa pemrograman utamapandasManipulasi dan analisis data tabularNumPyKomputasi numerik array/matriksscikit-learnPemodelan ML (SVM, KNN, RF), Preprocessing, & EvaluasiXGBoostAlgoritma Gradient Boosting classifierMatplotlib & SeabornVisualisasi data dan grafik statistikjoblibEkspor dan penyimpanan model .pkl
