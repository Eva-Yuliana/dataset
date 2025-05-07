# Laporan Proyek Machine Learning - Eva Yuliana

## Domain Proyek

Kanker payudara merupakan jenis kanker yang paling umum diderita oleh wanita di seluruh dunia. Diagnosis dini terhadap kanker payudara sangat penting untuk meningkatkan peluang kesembuhan dan mengurangi angka kematian. Namun, tidak semua rumah sakit umum memiliki fasilitas lengkap untuk melakukan diagnosis melalui mammogram. Untuk itu, pengembangan sistem diagnosis berbasis komputer dengan bantuan algoritma machine learning menjadi solusi alternatif yang cepat dan akurat.

Berdasarkan penelitian oleh Gayathri et al. (2013), berbagai metode machine learning telah digunakan untuk mendiagnosis kanker payudara dan membantu meningkatkan akurasi prediksi terhadap keberadaan kanker. Sistem ini diharapkan mampu membantu tenaga medis untuk mengambil keputusan lebih cepat dan akurat.

**Referensi:**
Gayathri, B. M., Sumathi, C. P., & Santhanam, T. (2013). *Breast cancer diagnosis using machine learning algorithms—a survey*. International Journal of Distributed and Parallel Systems. Diakses dari [academia.edu](https://www.academia.edu/5109296/Breast_Cancer_Diagnosis_Using_Machine_Learning_Algorithms_A_Survey)

## Business Understanding

### Problem Statements

* Bagaimana membangun model klasifikasi yang mampu membedakan antara kanker payudara jinak dan ganas secara akurat?
* Algoritma machine learning mana yang memberikan hasil terbaik pada dataset Breast Cancer Wisconsin?

### Goals

* Membangun model klasifikasi yang akurat untuk mendeteksi kanker payudara.
* Membandingkan performa dua model: Random Forest dan Logistic Regression dalam mendiagnosis kanker payudara.

### Solution Statements

* Menerapkan dua algoritma machine learning, yaitu Random Forest dan Logistic Regression.
* Melakukan evaluasi model berdasarkan metrik klasifikasi: akurasi, precision, recall, dan f1-score.

## Data Understanding

Dataset yang digunakan adalah **Breast Cancer Wisconsin (Diagnostic) Data Set** dari [Kaggle](https://www.kaggle.com/datasets/uciml/breast-cancer-wisconsin-data), yang berasal dari UCI Machine Learning Repository. Dataset ini berisi 569 sampel data dengan 30 fitur numerik dan label diagnosis (M = malignant/ganas, B = benign/jinak).

### Variabel-variabel pada dataset:

* `radius_mean`, `texture_mean`, `perimeter_mean`, `area_mean`, dst: statistik rata-rata dari masing-masing ciri sel kanker
* `diagnosis`: label target, M (malignant) atau B (benign)

## Data Preparation

Tahapan data preparation yang dilakukan:

* Menghapus kolom yang tidak relevan (`id` dan `Unnamed: 32`)
* Mengubah label diagnosis menjadi format biner (0 = benign, 1 = malignant)
* Melakukan feature scaling dengan StandardScaler untuk menormalkan data
* Membagi dataset menjadi training dan testing set (80:20 split)

Alasan dilakukan scaling adalah karena algoritma Logistic Regression sensitif terhadap skala fitur.

## Modeling

Dua algoritma digunakan untuk membangun model:

1. **Random Forest Classifier**

   * Model ensemble berbasis decision tree
   * Hyperparameter default digunakan

2. **Logistic Regression**

   * Model linear untuk klasifikasi biner
   * Solusi baseline karena sederhana dan interpretatif

## Evaluation

Metrik evaluasi yang digunakan:

* **Accuracy**: Persentase prediksi yang benar
* **Precision**: Proporsi prediksi positif yang benar-benar positif
* **Recall**: Proporsi kasus positif yang berhasil dikenali
* **F1-score**: Harmonik rata-rata precision dan recall

### Hasil Evaluasi:

**Random Forest Classifier**
![alt text](https://github.com/Eva-Yuliana/dataset/blob/main/Diagram.png?raw=true)

* Accuracy: 97.37%
* Confusion Matrix: \[\[72 0] \[3 39]]
* F1-score (class 1): 0.96

**Logistic Regression**

* Accuracy: 96.49%
* Confusion Matrix: \[\[71 1] \[3 39]]
* F1-score (class 1): 0.95

### Kesimpulan:

Kedua model menunjukkan performa tinggi, namun **Random Forest** sedikit lebih unggul dari segi f1-score dan akurasi, sehingga dipilih sebagai model terbaik untuk kasus ini.


