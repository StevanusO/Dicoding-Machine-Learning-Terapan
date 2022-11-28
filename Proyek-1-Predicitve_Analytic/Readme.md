# Laporan Proyek Machine Learning 
***
## Domain Proyek
***
### Latar Belakang
Sebagai respon dari pertumbuhan kebebasan berpendapat, informasi teks ini dapat ditemukan dimana saja, sebagai contoh di _blog post_, _e-commerce_, dan _website_.  

Sentimen, pendapat, opini, masukan dan kritik yang diberikan di contoh ini sangat bermanfaat sebagai sebuah indikator.[1] Secara umum sentimen ini dapat dikategorikan sebagai _postive_ dan _negative_ atau indikator yang lebih spesifik, sebagai contoh _anger_, _fear_, _joy_, _love_, _sadness_, dan surprise_ atau indikator lain.  

Dengan indikator diatas, sebuah tugas untuk menganalisa sentimen ini dapat di interpretasikan sebagai tugas klasifikasi dimana tiap kategori menyatakan sebuah sentimen. Analisa Sentimen ini berguna bagi perusahaan atau pemiliki usaha sebagai tolak ukur untuk mengukur seberapa diterimanya produk yang diberikan dan menentukan strategi untuk meningkatkan kualitas dari produk.[1]

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

![dataset_shape](https://user-images.githubusercontent.com/48939864/204278699-de1aea6d-ef74-44fe-8cd4-24656aa04c18.png)  
gambar 1. _Dataset Shape_    

![distribusi_train_numeric](https://user-images.githubusercontent.com/48939864/204278896-10524a1b-144f-4734-bbf4-3a3e14b04ea8.png)  
gambar 2. distribusi label pada **train_df**  

![distribusi_test_numeric](https://user-images.githubusercontent.com/48939864/204279020-0cb7fc61-8ab8-40bb-b72f-9d9dce104a4e.png)    
gambar 3. distribusi label pada **test_df**    

![distribusi_val_numeric](https://user-images.githubusercontent.com/48939864/204278968-9380058c-e8cc-4ace-9df0-d67c3146e902.png)    
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
- One Hot Encoding label
- Tokenisasi teks
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

Jika kita cek perubahan yang dilakukan dengan fungsi `head()` maka hasilnya akan seperti Tabel 3.  
Tabel 3. Tampilan _sample_ dari train_df setelah _text processing_ dilakukan.  
| text                                                | label   | clean_text                                        | encoded_label |
| --------------------------------------------------- | ------- | ------------------------------------------------- | ------------- |
| can go from feeling so hopeless to so damned...     | sadness | go feeling hopeless damned hopeful around some..  | 4             |
| i didnt feel humiliated                             | sadness | feel humiliated                                   | 4             |
| im grabbing a minute to post i feel greedy wrong    | anger   | grabbing minute post feel greedy wrong grabbin... | 0             |  

#### Merubah label menjadi numerik
Pada bagian ini variabel label akan dirubah dari kategorikal menjadi numerik. Variabel label memiliki 6 kategori yaitu _anger, fear, joy, love, sadness_ dan _surprise_. kategori ini akan dirubah menjadi numerik (0-5) dengan menggunakan `LabelEncoder`.   

Tabel 4. Label dirubah dengan LabelEncoder
| label    | label_encode |
| -------- | ------------ |
| anger    | 0            |
| fear     | 1            |
| joy      | 2            |
| love     | 3            |
| sadness  | 4            |
| surprise | 5            |


#### One Hot Encoding
Pada bagian ini variabel label dari 1 kolom, yang berisi 6 kategori akan menjadi 6 kolom yang memiliki nilai 0 dan 1 saja. Dengan proses ini mesin dapat menebak kategori yang ada di dataset. Untuk melakukan One Hot Encoding digunakan `to_categorical` dari _library keras.utils_

#### Tokenisasi
Pada bagian ini akan digunakan `Tokenizer, dan pad_sequences` dari _library tensorflow.keras_, Tujuan tokenisasi adalah untuk membuat kamus yang berisi indeks dari teks yang berisi tiap kata dan merubah kata menjadi _integer_. Pertama dimulai dnegan membuat kamus dari teks, teks yang akan digunakan hanya _DataFrame train_, penggunaan satu _DataFrame_ ini untuk mencegah agar mesin tidak seolah-olah mengetahui jawaban/kata yang ada di kamus saat dilakukan _test/val_ setelah dibuat kamus dengan `tokenizer.fit_on_texts(X_train)`, selanjutnya teks dari 3 _DataFrame_ akan dirubah menjadi _integer_ perubahan ini dapat dilakukan dengan memanggil fungsi `tokenizer.texts_to_sequence(X_train)`, `tokenizer.texts_to_sequence(X_test) dan `tokenizer.texts_to_sequence(X_val)`

Setelah teks di tokenisasi, teks di tiap _DataFrame_ perlu kita pastikan memiliki panjang yang sama, untuk melakukan itu digunakan fungsi `pad_sequences` dari _library tensorflow.keras_. teks dari 3 _DataFrame_ memiliki panjang 128, jika teks melebihi dari 128 maka bagian belakang akan dihapus.

## Modeling
***
#### Deep Learning
_Deep Learning_ adalah teknik yang menginzinkan model komputasi yang terdiri dari banyak _layer_ proses, _layer_ ini akan mempelajari representasi dari data dengan level abstraksi yang beragam. _Deep Learning_ menemukan struktur yang menarik dengan _dataset_ yang besar dengan menggunakan algoritma _backpropagation_, algoritma ini untuk mengindikasi bagaimana mesin harus mengganti parameter yang digunakan untuk menghitung tiap _layer_ dari representasi _layer_ sebelumnya.[3]
##### Tahapan umum Cara kerja Deep Learning
Data akan masuk ke _layer_ pertama, setelah itu di _layer_ pertama akan terdapat sejumlah neuron yang masing-masing akan memproses informasi yang telah diberikan, setiap neuron yang ada di _layer_ ini merepresentasikan informasi yang diproses, misal dengan dataset yang dipakai, neuron 1 bisa saja merepresentasikan sentimen _anger_, informasi yang terbentuk akan disalurkan ke _channel_ penghubung. Sebelum disalurkan dihitung nilai _weight & bias_ yang nilainya akan diterapkan di _activation function_. Hasil dari _activation function_ akan menentukan apakah neuron di _layer_ selanjutnya dapat diaktifkan. Setiap neuron yang diaktifkan akan meneruskan informasi ke _layer_ selanjutnya, ini berlanjut hingga _layer_ terakhir kedua, di layer terakhir kedua, hanya akan ada satu neuron yang diaktifkan untuk menentukan keluaran atau prediksi.

Pada kasus proyek ini bertipe _classification_ dan dataset adalah teks, jadi digunakan _deep learning_ dengan tipe _Biderectional Recurrent-Neural-Network (BRNN)_.
Manfaat dari tipe ini adalah model dapat mempelajari dan menghafal ketergantugan pola jangka panjang, tipe ini dapat mengingat/menggunakan informasi di layer.
yang membuat BRNN menarik adalah terdapat 2 RNN yang independen, RNN 1 diberikan input dari layer pertama ke terakhir dan di RNN 2 terbalik. Keluaran dari 2 RNN ini akan digabungkan tiap kali 1 perulangan. Tipe ini mengizinkan jaringan saraf tiruan untuk diberikan informasi _backward_ dan _forward_ setiap perulangan.
Arsitektur Model yang digunakan adalah sebagai berikut:
1. _Layer Input_ (Embedding) akan ada 14977 neuron untuk menerima data _input_ dan 64 neuron untuk ke _layer_ selanjutnya.  
2. hidden layer 1 (Biderectional LSTM) dengan 128 neuron, `return_sequences = True` artinya keluaran dari hidden layer ini akan mengembalikan sebuah _output_ di _layer_ selanjutnya.  
3. hidden layer 2 (Biderectional LSTM) dnegan 256 neuron.  
4. _Layer Output_ (Dense) yang akan menerima 6 neuron atau setara dengan jumlah kategori yang ada pada label.  
rangkuman dari arsitektur dapat dilihat di tabel 5.  
Tabel 5. Rangkuman _Model_.  
| *layer* | Jenis *layer*   | *Neuron*                 |
| ------- | --------------  | ------------------------ |
|    1    |  *Input*        | Input: 14977, Output: 64 |
|    2    |  *Hidden Layer* | 128                      |
|    3    |  *Hidden Layer* | 256                      |
|    4    |  *Output*       | 6                        |

## Evaluasi
***
Pada proyek ini menggunakan model _deep learning_ bertipe _classification_ yang berarti jika mendekati 100% accuracy, performanya baik, sedangkan jika dibawah 75%, maka performanya buruk.
Metrik yang akan kita gunakan pada prediksi ini adalah _Accuracy_, metrik ini menghitung jumlah prediksi yang benar selisih total prediksi yang dilakukan. Accuracy didefinisikan dalam persamaan berikut:  
$\text{Accuracy} = \frac{TP+TN}{TP+TN+FP+FN}$   

Selain metrik _accuracy_ akan digunakan _precision, recall, dan f1-score_ yang dibuat dengan fungsi *classification_report* yang disediakan oleh _library sklearn_  

Presisi digunakan untuk mengukur seberapa dapat diandalkan sebuah model ketika memberikan prediksi terhadap suatu kelas/_target_. Presisi dapat didefinisikan sebagai berikut:  
$\text{Precision} = \frac{TP}{TP+FP}$

_Recall_ digunakan untuk mengukur kemampuan model untuk memprediksi kelas _True Positive. Recall_ dapat didefinisikan sebagai berikut:  
$\text{Recall} = \frac{TP}{TP+FN}$  

_F1-Score_ digunakan untuk mencari titik seimbang antara Presisi dan _Recall_, _F1-Score_ didefinisikan sebagai berikut:  
$\text{F1-Score} = \frac{2 \* Precision \* Recall}{Precision+Recall}$    

Dengan:
- TP: True Positive
- TN: True Negative
- FP: False Positive
- FN: False Negative

![model_accuracy](https://user-images.githubusercontent.com/48939864/204292084-ff41b8d6-5ca5-4959-8681-a7e820f97d9e.png)  
gambar 5 Model Accuracy Plot  

Dapat dilihat dari gambar 5 bahwa setelah _epochs_ ke 200 model membuat model yang _Good Fit_ dengan nilai akurasi _train_ : 99% dan akurasi validasi: 90%  

Penulis juga menguji model dengan data _test_ yang sebelumnya sudah dipisahkan dengan hasil seperti berikut gambar 6.  

![classification_report](https://user-images.githubusercontent.com/48939864/204292922-080dd86c-e5a3-4d89-9c91-0e8ccabebf8c.png)  
gambar 6. _Classification Report_  

Terlihat bahwa model bekerja dengan baik, dari keenam label yang diprediksi didapat seluruh nilai diatas 70%, dengan akurasi test sebesar 90%.
- Precision
  - anger
  dari 275 data yang model prediksi, 91% diprediksi memiliki perasaan marah.    
  - fear
  dari 224 data yang model prediksi, 89% diprediksi memiliki perasaan ketakutan.    
  - joy
  dari 695 data yang model prediks,i 92% diprediksi memiliki perasaan senang.  
  - love
  dari 159 data yang model prediksi, 71% diprediksi memiliki perasaan cinta/suka.  
  - sadness
  dari 581 data yang model prediksi, 93% diprediksi memiliki perasaan sedih.  
  - surprise
  dari 66 data yang model prediksi, 82% diprediksi memiliki perasaan terkejut.  
  
- Recall
- anger
  dari 91% yang diprediksi memiliki perasaan marah, hanya 88% menghasilkan benar. 
  - fear
  dari 89% yang diprediksi memiliki perasaan ketakutan, hanya 86% menghasilkan benar. 
  - joy
  dari 92% yang diprediksi memiliki perasaan senang, hanya 92% menghasilkan benar. 
  - love
  dari 71% yang diprediksi memiliki perasaan cinta/suka, hanya 81% menghasilkan benar. 
  - sadness
  dari 93% yang diprediksi memiliki perasaan sedih, hanya 94% menghasilkan benar. 
  - surprise
  dari 82% yang diprediksi memiliki perasaan terkejut, hanya 71% menghasilkan benar.  
  
- F1-Score
Dari keenam label, dapat dilihat bahwa model menghasilkan performa yang baik, terutama pada label sadness dan joy karena hampir mendekati 100%, untuk label love dan surprise mendapatkan nilai 76% dapat disebabkan karena jumlah data dengan label tersebut tidak banyak.

- Kesimpulan
Dari hasil gambar 5 kita dapat melihat bahwa model mendapatkan performa yang baik dalam _train_ dengan akurasi 99% dan validasi 90%, performa baik ini juga dibuktikan dengan evaluasi _model_ menggunakan data _test_ yang disiapkan. Dari data _test_ dapat dibuat _classification report_ yang ada di gambar 6. Dari gambar 6 kita dapat melihat skor dari _model_ terhadap 3 metrik yang di _generate_ oleh _classification report_, dilihat dari hasil dapat disimpulkan bahwa _model_ yang dibuat _Good Fit_.
Referensi:  
  [1]    
  [Prabowo, Rudy, and Mike Thelwall. “Sentiment Analysis: A Combined Approach.” Journal of Informetrics, vol. 3, no. 2, 2009, pp. 143–157., https://doi.org/10.1016/j.joi.2009.01.003.](https://www.sciencedirect.com/science/article/abs/pii/S1751157709000108)
  [2]  
  [Grefenstette, Gregory. “Tokenization.” Text, Speech and Language Technology, 1999, pp. 117–133., https://doi.org/10.1007/978-94-015-9273-4_9.](https://link.springer.com/chapter/10.1007/978-94-015-9273-4_9)
  [3]  
  [LeCun, Yann, et al. “Deep Learning.” Nature News, Nature Publishing Group, 27 May 2015, https://www.nature.com/articles/nature14539.](https://www.nature.com/articles/nature14539#citeas)
