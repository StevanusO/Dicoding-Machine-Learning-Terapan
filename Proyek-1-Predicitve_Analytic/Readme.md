# Laporan Proyek Machine Learning 
***
## Domain Proyek
***
### Latar Belakang
Sebagai respon dari pertumbuhan kebebasan berpendapat, informasi teks ini dapat ditemukan dimana saja, sebagai contoh di _blog post_, _e-commerce_, dan _website_.  

Sentimen, pendapat, opini, masukan dan kritik yang diberikan di contoh ini sangat bermanfaat sebagai sebuah indikator.[1] Secara umum sentimen ini dapat dikategorikan sebagai _postive_ dan _negative_ atau indikator yang lebih spesifik, sebagai contoh _anger_, _fear_, _joy_, _love_, _sadness_, dan surprise_ atau indikator lain.  

Dengan indikator diatas, sebuah tugas untuk menganalisa sentimen ini dapat di interpretasikan sebnagai tugas klasifikasi dimana tiap kategori menyatakan sebuah sentimen. Analisa Sentimen ini berguna bagi perusahaan atau pemiliki usaha sebagai tolak ukur untuk mengukur seberapa diterimanya produk yang diberikan dan menentukan strategi untuk meningkatkan kualitas dari produk.[1]

Dalam praktiknya, analisis sentimen bisa dilakukan dengan melihat kata demi kata pada kalimat dan mencermati arti dari kata, praktik ini cukup merepotkan dan memakan banyak dilakukan jika sentimen yang diberikan terlalu banyak, maka dari itu dibuatlah sebuah algoritma untuk prediksi kategori dari sentimen yang diberikan oleh individu, algoritma yang dibuat adalah dengan membuat _model Deep Learning_ yang nanti akan dilatih dan di_test_ dengan 20000 data teks.
## Business Understanding
***
### Problem Statements
Berdasarkan latar belakang di atas, berikut ini batasan masalah yang dapat diselesaikan dengan proyek ini:
- Bagaimana cara melakukan pra-pemrosesan data agar dapat digunakan untuk melatih _model_?
- Bagaiman cara membuat arsitektur _model_ yang akan digunakan untuk memprediksi?

### Goals
- Melakukan pre-pemrosesan data dengan baik agar dapat digunakan
- Mengetahui cara membuat _model deep learning_ untuk memprediksi sentimen yang diberikan oleh individu

### Solution Statements
Solusi yang dapat dilakukan sebagai berikut:
- Membuat _model deep learning_
- Menggunakan _Classifictaion Report_ untuk mengevaluasi model saat testing dan accuracy saat train.
## Data Understanding
***
Dataset yang digunakan dapat diakses menggunakan [Kaggle](https://www.kaggle.com/datasets/praveengovi/emotions-dataset-for-nlp)  
Informasi dari dataset dapat dirangkum sebagai berikut:
Tabel 1. Rangkuman informasi Dataset    
| Jenis                  | Keterangan                                                                                                        |
| ---------------------- | ------------                                                                                                      |
| Sumber                 | [Kaggle Dataset: Emotions dataset for NLP](https://www.kaggle.com/datasets/praveengovi/emotions-dataset-for-nlp)  |
| Lisensi                | [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)                                                   |
| Kategori               | Sosial                                                                                                            |
| Jenis & Ukuran berkas  | TXT (2.07MB)                                                                                                      |  
***
Pada berkas yang diunduh berisi 3 berkas dengan jenis format _.txt_ yang masing-masing adalah _train.txt, test.txt, val.txt_ dengan masing-masing berisi 16000, 2000, 2000 teks dan label. 3 berkas masing-masing memiliki 2 kolom yang bertipe kategorikal(tipe data _object_). Untuk penjelasan mengenai variabel pada dataset sebagai berikut:  
- Text: kalimat/sentimen/pendapat/kritik yang ditulis oleh individu
- Label: perasaan yang dirasakan oleh individu. 
***
### Langkah-langkah pra-pemrosesan data
1. Mendownload _dataset_ dari kaggle
2. Membaca _dataset_ yang telah didownload ke _DataFrame menggunakan _pandas_
3. Menampilkan informasi dari _dataset_
4. Mengecek dan mengani missing value di _dataset_ (jika ditemukan).
5. Mengecek _sample text_ yang ada di _DataFrame_

### Mendownload dari kaggle
Pada proyek ini _dataset_ di download melalui kaggle, untuk mendownload _dataset_ digunakan sebuah _library_ bernama _opendatasets_, selanjutnya dari _library_ akan di _import_ ke code cell dan disingkat sebagai _od_, selanjutnya tinggal memanggil function _downlaod_ pada _od_ seperti berikut:  
`od.download('https://www.kaggle.com/datasets/praveengovi/emotions-dataset-for-nlp')`  
setelah di _run_ akan diminta _username_ dan kaggle.json _key_.
### Membaca _dataset_ ke _DataFrame pandas_
Pada bagian ini akan digunakan `pandas.read_csv()` untuk membaca berkas txt, karena berkas bersifat txt, tidak memiliki _header_ dan pemisah antara variabel _text_ dan _label_ adalah ";" maka kita dapat menulisnya sebagai berikut:  
`train_df = pd.read_csv("../content/emotions-dataset-for-nlp/train.txt", sep=';', header=None, names=['text', 'label'])`    

`test_df = pd.read_csv("../content/emotions-dataset-for-nlp/test.txt", sep=';', header=None, names=['text', 'label'])`  

`val_df = pd.read_csv("../content/emotions-dataset-for-nlp/val.txt", sep=';', header=None, names=['text', 'label'])`  
Setelah 3 berkas dibaca dan disimpan di 3 variabel **train_df**, **test_df** dan **val_df**, akan dilihat _sample_ data dari **train_df** dengan menggunakan `train_df.head()`, lalu tampilannya akan seperti tabel 2.

Tabel 2. Tampilan _sample_ dari dataset **train_df** dengan bentuk _DataFrame pandas_.  
|   | text                                                 | label   |
| - | ---------------------------------------------------- | ------- |
| 0 | i didnt feel humiliated                              | sadness |
| 1 | i can go from feeling so hopeless to so damned..     | sadness |
| 2 | im grabbing a minute to post i feel greedy wrong	a  | anger   |
| 3 | i am ever feeling nostalgic about the fireplac..     | love    |
| 4 | i am feeling grouchy                                 |  anger  |
### Menampilkan informasi dari dataset
Pada bagian ini akan digunakan fungsi shape() dan value_counts() untuk mengetahui jumlah dataset dan distribusi dari label, informasi dari jumlah dan distribusi dapat dilihat pada gambar 1-4.    

![dataset_shape](https://github.com/StevanusO/Dicoding-Machine-Learning-Terapan/blob/main/Proyek-1-Predicitve_Analytic/img/dataset_shape.png)  
gambar 1. _Dataset Shape_    

![distribusi_label_train](https://github.com/StevanusO/Dicoding-Machine-Learning-Terapan/blob/main/Proyek-1-Predicitve_Analytic/img/distribusi_train_numeric.png)  
gambar 2. distribusi label pada **train_df**  

![distribusi_label_test](https://github.com/StevanusO/Dicoding-Machine-Learning-Terapan/blob/main/Proyek-1-Predicitve_Analytic/img/distribusi_test_numeric.png)   
gambar 3. distribusi label pada **test_df**    

![distribusi_label_val](https://github.com/StevanusO/Dicoding-Machine-Learning-Terapan/blob/main/Proyek-1-Predicitve_Analytic/img/distribusi_val_numeric.png)   
gambar 4. distribusi label pada **val_df**    

### Mengecek missing value dan menangani jika ditemukan
Pada bagian ini digunakan fungsi `isnull().sum()` untuk tiap _DataFrame_. Saat dicek tidak ditemukan adanya _missing value_ pada 3 _DataFrame_

### Mengecek _sample text_ yang ada di _DataFrame_
pada bagian ini akan diambil satu _sample_ teks dari masing-masing _DataFrame_, untuk mengambil satu _sample_ digunakan index. 
`sample_train = train_df['text'][0]`  

`sample_test = test_df['text'][0]`  

`sample_val = val_df['text'][0]`  

Setelah itu akan di _print_ untuk mengecek _sample_ dari teks
`print("train sample txt:", sample_train)`  

`print("test sample txt:", sample_test)`  

`print("val sample txt:", sample_val)`  

_Output:_
> train sample txt: i didnt feel humiliated  
> test sample txt: im feeling rather rotten so im not very ambitious right now  
> val sample txt: im feeling quite sad and sorry for myself but ill snap out of it soon  

Dari hasil _output_ dapat dilihat bahwa teks yang diambil dari masing-masing dataset masih perlu diprocess karena mengandung kata-kata yang bisa dirubah atau dapat dihapus.
***
## Data Preparation
***
### Tahap _Prepation_:
- Menghapus angka yang ada di variabel _text_ 
- Menghapus tanda baca yang ada di variabel _text_
- Merubah tiap kata di variabel _text_ menjadi bentuk dasar
- Merubah kata menjadi _lowercase_ pada variabel _text_
- Menghapus _stopwords_ pada variabel _text_
- Merubah variabel label menjadi numerik
#### _Text Processing_
Pada bagian ini, teks yang ada akan di _process_ untuk menghapus, merubah dan _lowercase_, untuk melakukan itu digunakan beberapa _library_ yaitu _re, nltk dan pandas_
Dibuat sebuah fungsi baru yang bernama *clean_text* yang tugasnya adalah memanggil fungsi yang ada pada 3 _library_.   

_lowercase_ teks menggunakan _pandas_
`text.lower()`    

Menghapus angka menggunakan _re_ atau _regular expression_  
`num = re.compile(r'[-+]?[.\d]*[\d]+[:,.\d]*')`  
`num.sub(r'', text)`  

Menghapus tanda baca menggunakan _re_    
`punctuations = '@#!?+&*[]-%.:/();$=><|{}^'`   
`for p in punctuations:`     
 `  text = text.replace(p, f' {p} ') `      
 
Merubah kata menjadi bentuk dasar menggunakan _nltk.stem.WordNetLemmatizer_     
`lemmatizer = WordNetLemmatizer()#panggil fungsi WordNet dari nltk`  
`stop_words = [word for word in text.split() if word not in (stopwords)]`    
`text = ' '.join([lemmatizer.lemmatize(contractions.fix(lower_text(text))) for txt in text.split() if txt not in stop_words])`    

Menghapus _stopwords_ menggunakan _nltk.corpus.stopwords_  
`stopwords = stopwords.words('english') #panggil stopwords dan set ke bahasa inggris`    
`text = ' '.join([word for word in text.split() if word not in (stopwords)])`    

Jika kita cek perubahan yang dilakukan dengan fungsi `head()` maka hasilnya akan seperti gambar 5.  


Referensi:  
  [1]   
  [Prabowo, Rudy, and Mike Thelwall. “Sentiment Analysis: A Combined Approach.” Journal of Informetrics, vol. 3, no. 2, 2009, pp. 143–157., https://doi.org/10.1016/j.joi.2009.01.003.](https://www.sciencedirect.com/science/article/abs/pii/S1751157709000108)
