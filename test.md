# Laporan Proyek Machine Learning - Eva Yuliana

## Domain Proyek

Kanker payudara merupakan salah satu penyebab utama kematian akibat kanker pada wanita di seluruh dunia. Deteksi dini memiliki peran krusial dalam meningkatkan tingkat kesembuhan dan menurunkan angka kematian. Sayangnya, tidak semua fasilitas layanan kesehatan memiliki teknologi yang cukup canggih untuk mendeteksi kanker payudara melalui metode radiologis seperti mammogram.

Oleh karena itu, solusi alternatif berbasis *Machine Learning* sangat dibutuhkan untuk membantu proses diagnosis dengan cepat dan akurat menggunakan data medis yang telah tersedia. Pendekatan ini juga dapat membantu tenaga medis dalam pengambilan keputusan, terutama di daerah dengan keterbatasan alat medis.

### Referensi:

Gayathri, B. M., Sumathi, C. P., & Santhanam, T. (2013). *Breast Cancer Diagnosis Using Machine Learning Algorithms – A Survey*. International Journal of Distributed and Parallel Systems.
[Link ke sumber](https://www.academia.edu/5109296/Breast_Cancer_Diagnosis_Using_Machine_Learning_Algorithms_A_Survey)

## Business Understanding

### Problem Statements

* Bagaimana membangun model klasifikasi yang dapat secara akurat membedakan antara kanker payudara jinak (benign) dan ganas (malignant)?
* Algoritma machine learning mana yang memberikan hasil terbaik dalam mendeteksi kanker payudara pada dataset Breast Cancer Wisconsin?

### Goals

* Membangun model klasifikasi kanker payudara yang akurat dan dapat diandalkan.
* Membandingkan performa algoritma Random Forest dan Logistic Regression untuk diagnosis kanker payudara.

### Solution Statements

* Menerapkan dua algoritma Machine Learning: **Random Forest Classifier** dan **Logistic Regression**.
* Melakukan evaluasi performa model berdasarkan metrik: accuracy, precision, recall, dan f1-score.
* Memilih model terbaik berdasarkan metrik evaluasi.
* (Tambahan) Model baseline Logistic Regression juga akan dibandingkan dengan Random Forest tanpa dan dengan tuning sederhana.

## Data Understanding

Dataset yang digunakan adalah **Breast Cancer Wisconsin (Diagnostic) Data Set**, tersedia di Kaggle:

📂 Link Dataset: [https://www.kaggle.com/datasets/uciml/breast-cancer-wisconsin-data](https://www.kaggle.com/datasets/uciml/breast-cancer-wisconsin-data)

### Informasi Umum:

* Jumlah sampel: **569**
* Jumlah fitur: **30 fitur numerik**
* Label target: `diagnosis` (M = Malignant, B = Benign)

### Penjelasan Variabel:

Fitur mencerminkan karakteristik dari inti sel kanker yang diukur dari citra digital hasil biopsi:

* `radius_mean`, `texture_mean`, `perimeter_mean`, `area_mean`, `smoothness_mean`, dst.
* Tiga kelompok statistik fitur: *mean*, *standard error (se)*, dan *worst* (nilai maksimum).
* Label `diagnosis`: target klasifikasi (B=0, M=1)

### Exploratory Data Analysis (EDA) - Ringkasan:

* Kelas data seimbang: 212 ganas (malignant), 357 jinak (benign)
* Korelasi tinggi antar beberapa fitur (misalnya radius dan area)
* Boxplot menunjukkan perbedaan distribusi fitur antara dua kelas diagnosis

## Data Preparation

Langkah-langkah yang dilakukan:

1. **Menghapus kolom tidak relevan**:

   * `id` dan `Unnamed: 32` dihapus karena tidak berkontribusi pada prediksi.

2. **Encoding Label Target**:

   * Diagnosis dikonversi: `M` → 1 (ganas), `B` → 0 (jinak).

3. **Feature Scaling**:

   * Menggunakan `StandardScaler` untuk menormalkan fitur agar Logistic Regression bekerja optimal.

4. **Split Dataset**:

   * Dataset dibagi menjadi: 80% data latih (`train`), 20% data uji (`test`) dengan `stratify` agar proporsi label seimbang.

### Alasan Dilakukan:

* Scaling penting untuk algoritma seperti Logistic Regression yang berbasis pada perhitungan jarak.
* Encoding diperlukan agar model bisa membaca label target.
* Stratified split menjaga distribusi kelas tetap proporsional.


## Modeling

Dua model digunakan untuk membandingkan performa:

### 1. Random Forest Classifier

* Algoritma *ensemble learning* berbasis pohon keputusan.
* Kelebihan:

  * Tahan terhadap overfitting.
  * Tidak memerlukan scaling fitur.
* Kekurangan:

  * Interpretasi hasil tidak semudah model linear.
* Parameter:

  * Menggunakan default (`n_estimators=100`, `max_depth=None`, dll).

### 2. Logistic Regression

* Model klasifikasi linear untuk kasus biner.
* Kelebihan:

  * Sederhana, cepat dilatih, dan interpretatif.
* Kekurangan:

  * Kurang baik jika terdapat relasi non-linear.
* Parameter:

  * `solver='liblinear'` (cocok untuk dataset kecil), `C=1.0`


## Evaluation

### Metrik Evaluasi yang Digunakan:

1. **Accuracy**
   $\text{Accuracy} = \frac{TP + TN}{TP + TN + FP + FN}$

2. **Precision**
   $\text{Precision} = \frac{TP}{TP + FP}$

3. **Recall**
   $\text{Recall} = \frac{TP}{TP + FN}$

4. **F1-score**
   $F1 = 2 \cdot \frac{\text{Precision} \cdot \text{Recall}}{\text{Precision} + \text{Recall}}$


### Hasil Evaluasi

#### Random Forest Classifier

![Diagram](https://github.com/Eva-Yuliana/dataset/blob/main/Diagram.png?raw=true)
![Confusion Matrix](https://github.com/Eva-Yuliana/dataset/blob/main/Matrix.png?raw=true)

* **Accuracy**: 97.37%
* **Precision (class 1)**: 0.97
* **Recall (class 1)**: 0.93
* **F1-score (class 1)**: 0.96
* **Confusion Matrix**:

  ```
  [[72  0]
   [ 3 39]]
  ```

#### Logistic Regression

* **Accuracy**: 96.49%
* **Precision (class 1)**: 0.97
* **Recall (class 1)**: 0.93
* **F1-score (class 1)**: 0.95
* **Confusion Matrix**:

  ```
  [[71  1]
   [ 3 39]]
  ```

### Kesimpulan

Kedua model menunjukkan performa yang sangat baik pada dataset Breast Cancer Wisconsin. Namun:

* **Random Forest Classifier** sedikit lebih unggul dalam hal *f1-score* dan *accuracy* dibanding Logistic Regression.
* Oleh karena itu, **Random Forest** dipilih sebagai model akhir untuk digunakan dalam deteksi kanker payudara.

## Penutup

Model ini dapat dikembangkan lebih lanjut dengan:

* Tuning hyperparameter Random Forest untuk hasil lebih optimal.
* Menambahkan teknik seleksi fitur untuk mengurangi dimensi data.
* Uji model dengan data baru dari sumber berbeda untuk mengevaluasi generalisasi.

