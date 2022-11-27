# Laporan Proyek Machine Learning - Stevanus Ong

## Domain Proyek
Sebagai respon dari pertumbuhan terhadap ketersedian informasi, opini teks seperti _blog post_  dan _product review_ di sebuah _website_, studi _Sentiment Analysis_ muncul untuk menjawab untuk menjawab satu pertanyaan yaitu _Apa yang orang lain pikirkan terhadap suatu topik atau produk?_ [1] Salah satu upaya untuk menjawab pertanyaan ini adalah dengan membuat model Deep Learning.

Referensi:

  1. [Sentiment Analysis: An Overview](https://www.academia.edu/download/3243118/CompsYelenaMejova.pdf)

## Business Understanding
### Problem Statements
Adapun masalah yang diangkat sebagai berikut:
- Apa yang orang lain pikirkan terhadap suatu topik atau produk?

### Goals
Adapun tujuan dari proyek ini adalah:
- Menggunakan Deep Learning untuk mendekteksi apa yang dipikirkan orang lain

### Solution Statements
Adapun Solusi yang penulis tawarkan sebagai berikut:
- Membangun model deep learning yang mampu mendeteksi perasaan orang lain berdasarkan teks yang diberikan
- Menggunakan Classification Report (Precision, Recall, Accuracy dan F1-Score) untuk mengevaluasi model yang dibuat

## Data Understanding
Data yang digunkaan untuk melatih model dapat didownload melalui [Kaggle](https://www.kaggle.com/datasets/praveengovi/emotions-dataset-for-nlp)

Variabel pada dataset Emotions dataset for NLP adalah sebagai berikut:
- Teks: string yang isinya berupa kalimat atau perasaan
- Label: Perasaan atau target yang akan ditebak, ada 6 label sebagai berikut:
  - 0: anger 
  - 1: fear 
  - 2: joy 
  - 3: love 
  - 4: sadness 
  - 5: surprise 
  
### Exploratory Data Analysis
Disini dapat dilihat bahwa dataset secara default sudah terbagi menjadi Train (80%), Test (10%) dan Val (10%):

![Dataset_Shape](https://github.com/StevanusO/Dicoding-Machine-Learning-Terapan/blob/c826104afd578f7e9d16acf17b9943a734105cbd/Proyek-1-Predicitve_Analytic/img/dataset_shape.png)

#### Distribusi dari Label pada Train, Test dan Val
- Train   
![Distribusi_pada_train_df_numeric](https://github.com/StevanusO/Dicoding-Machine-Learning-Terapan/blob/a469ab8c1b265a637d7893ed28ee7d03093bca38/Proyek-1-Predicitve_Analytic/img/distribusi_train_numeric.png)

Distribusi pada train_df plot  
<picture>
  <source media="(prefers-color-scheme: light)" srcset="https://github.com/StevanusO/Dicoding-Machine-Learning-Terapan/blob/main/Proyek-1-Predicitve_Analytic/img/distribusi_train_plot.png">
  <source media="(prefers-color-scheme: dark)" srcset="https://github.com/StevanusO/Dicoding-Machine-Learning-Terapan/blob/main/Proyek-1-Predicitve_Analytic/img/distribusi_train_plot.png">
  <img alt="Distribusi train_df plot." src="https://github.com/StevanusO/Dicoding-Machine-Learning-Terapan/blob/main/Proyek-1-Predicitve_Analytic/img/distribusi_train_plot.png">
</picture>

- Test 
Distribusi pada test_df  
![Distribusi_pada_test_df_numeric](https://github.com/StevanusO/Dicoding-Machine-Learning-Terapan/blob/main/Proyek-1-Predicitve_Analytic/img/distribusi_test_numeric.png)

Distribusi pada test_df plot  
<picture>
  <source media="(prefers-color-scheme: light)" srcset="https://github.com/StevanusO/Dicoding-Machine-Learning-Terapan/blob/main/Proyek-1-Predicitve_Analytic/img/distribusi_test_plot.png">
  <source media="(prefers-color-scheme: dark)" srcset="https://github.com/StevanusO/Dicoding-Machine-Learning-Terapan/blob/main/Proyek-1-Predicitve_Analytic/img/distribusi_test_plot.png">
  <img alt="Distribusi train_df plot." src="https://github.com/StevanusO/Dicoding-Machine-Learning-Terapan/blob/main/Proyek-1-Predicitve_Analytic/img/distribusi_test_plot.png">
</picture>

- Val
Distribusi pada val_df  
![Distribusi_pada_val_df_numeric](https://github.com/StevanusO/Dicoding-Machine-Learning-Terapan/blob/628992cd839225b3eb1894a33e4f4f8834cc8b4e/Proyek-1-Predicitve_Analytic/img/distribusi_val_numeric.png)

Distribusi pada val_df plot  
<picture>
  <source media="(prefers-color-scheme: light)" srcset="https://github.com/StevanusO/Dicoding-Machine-Learning-Terapan/blob/main/Proyek-1-Predicitve_Analytic/img/distribusi_val_plot.png">
  <source media="(prefers-color-scheme: dark)" srcset="https://github.com/StevanusO/Dicoding-Machine-Learning-Terapan/blob/main/Proyek-1-Predicitve_Analytic/img/distribusi_val_plot.png">
  <img alt="Distribusi train_df plot." src="https://github.com/StevanusO/Dicoding-Machine-Learning-Terapan/blob/main/Proyek-1-Predicitve_Analytic/img/distribusi_val_plot.png">
</picture>

Dari gambar distribusi dari label, dapat dilihat bahwa terdapat ketidakseimbangan pada label, khususnya pada label _surprise_. Untuk kasus ini tidak dilakukan _balancing class_ dikarenakan model yang dibuat dapat melakukan prediksi dengan performa yang baik.
## Data Preparation
- Merubah label menjadi dari kategorikal menjadi data yang dimengerti mesin, yaitu angka
- Mengubah teks menjadi tidak _lowercase_
- Menghapus angka dari teks
- Menghapus tanda baca dari teks
- Menghapus _Stopwords_ dari teks
- Merubah kata pada teks menjadi bentuk dasar
- Tokenisasi dataset
## Modeling
Penulis membuat arsitektur deep learning yang dapat dilihat sebagai berikut:  
![Model_Summary](https://github.com/StevanusO/Dicoding-Machine-Learning-Terapan/blob/main/Proyek-1-Predicitve_Analytic/img/model_summary.png)  
Dari gambar diatas dapat dilihat, terdapat 4 bagian, yaitu bagian masukan(embedding), bagian hidden_layer_1(Biderectional), bagian hidden_layer_2(Biderectional) dan bagian keluaran(Dense)   
## Evaluation


