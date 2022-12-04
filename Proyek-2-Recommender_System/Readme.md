# Laporan Proyek Machine Learning 
***
## Project Overview

Buku adalah jendela dunia. Dengan membaca buku seseorang dapat memperoleh ilmu yang tiada batas, tanpa ada batasan waktu, dan mengenal seseorang dari seluruh sisi dunia, karena buku merupakan sumber ilmu pengetahuan. Untuk dapat memperoleh ilmu yang ada di dalam buku, seseorang harus membaca buku.[1] Kegiatan membaca buku ini sangat penting bagi manusia, dengan terbiasa membaca buku, maka seseorang akan memiliki pengetahuan yang luas. Namun dengan banyaknya jumlah buku yang tersedia terkadang membuat pembaca kebingungan dalam menentukan buku yang akan dibaca. Ada pula pembaca yang hanya ingin membaca buku yang mirip dengan yang pernah dibaca sebelumnya. Tidak jarang juga ditemui pembaca yang menentukan buku-buku yang akan dibaca selanjutnya berdasarkan jenis dari bukunya, semakin berbeda jenis bukunya semakin enggan pembaca buku.

Berdasarkan permasalahan tersebut, pada proyek ini akan dibuat suatu model sistem rekomendasi menggunkaan _content-based filtering_ untuk merekomendasikan buku-buku yang mungkin akan dibaca oleh pengguna. _Content-based filtering_ merupakan metode yang digunakan untuk merekomendasikan _item_ berdasarkan "fitur" dari _item_ berdasarkan dari aksi atau _explicit feedback_ sebelumnya. Contohnya yaitu merekomendasikan suatu film berdasarkan tokoh utamanya. Dengan adanya sistem rekomendasi ini diharapkan dapat membantu pembaca untuk menentukan buku yang akan dibaca selanjutnya.

## Business Understanding
***
### Problem Statements
Berdasarkan penjelasan pada _project overview_, berikut merupakan rincian masalah yang perlu diselesaikan di proyek ini:
- Sistem rekomendasi apa yang baik diterapkan pada kasus ini?
- Bagaimana cara membuat sistem rekomendasi buku yang akan merekomendasikan buku berdasarkan jenis/genre dari buku?

### Goals
Tujuan dibuatnya proyek ini adalah sebagai berikut:
- Membuat sistem rekomendasi buku dengan jenis buku sebagai fitur.
- Memberikan rekomendasi buku yang mungkin disukai pengguna.

### Solution Approach
Solusi yang dapat dilakukan untuk memenuhi tujuan dari proyek ini diantaranya:
- Membuat sebuah model sistem rekomendasi 
- Mengevaluasi hasil rekomendasi yang diberikan
  
## Data Understanding
***
Dataset yang digunakan dapat diakses menggunakan [kaggle](https://www.kaggle.com/datasets/ruchi798/bookcrossing-dataset)  
Informasi dari dataset dapat dilihat di Tabel 1.  
Tabel 1. Rangkuman informasi Dataset

| Jenis                  | Keterangan                                                                                                        |
| ---------------------- | ----------------------------------------------------------------------------------------------------------------- |
| Sumber                 | [Book-Crossing: User review ratings](https://www.kaggle.com/datasets/ruchi798/bookcrossing-dataset)               |
| Lisensi                | [CC0: Public Domain](https://creativecommons.org/publicdomain/zero/1.0/)                                          |
| Kategori               | Arts and Entertainment, Online Communities, Literature                                                            |
| Jenis & Ukuran berkas  | ZIP (600.34 MB)                                                                                                   |  
***
Setelah melakukan observasi pada dataset yang diunduh pada kaggle, didapat informasi sebagai berikut:
- Terdapat 1031175 baris dalam _dataset_
- Terdapat 19 kolom yaitu 'Unnamed: 0', 'user_id', 'location', 'age', 'isbn', 'rating', 'book_title', 'book_author', 'year_of_publication', 'publisher', 'img_s', 'img_m', 'img_l', 'Summary', 'Language', 'Category', 'city', 'state', 'country'.  

Untuk penjelasan mengenai 19 kolom yaitu sebagai berikut:  
- `user_id` : id dari pengguna
- `location` : lokasi/alamat pengguna
- `age` : umur pengguna
- `isbn` : kode ISBN (International Standard Book Number) buku
- `rating` : rating dari buku
- `book_title` : judul buku
- `book_author` : penulis buku
- `year_of_publication` : tahun terbit buku
- `publisher` : penerbit buku
- `img_s` : gambar sampul buku (ukuran kecil)
- `img_m` : gambar sampul buku (ukuran sedang)
- `img_l` : gambar sampul buku (ukuran besar)
- `Summary` : ringkasan/sinopsis buku
- `Language` : bahasa yang digunakan buku
- `Category` : kategori buku
- `city` : kota pengguna
- `state` : negara bagian penguna
- `country` : negara pengguna
***
### Data Exploration
Tabel 2. Sample Data

| Unnamed: 0 | user_id | location | age | isbn | rating | book_title | book_author | year_of_publication | publisher | img_s | img_m | img_l | summary | language | category | city | state | country |  
| ------------ | ------------ | ------------ | ------------ | ------------ | ------------ | ------------ | ------------ | ------------ | ------------ | ------------ | ------------ | ------------ | ------------ | ------------ | ------------ | ------------ | ------------ | ------------ | 
| 0 | 0 | 2 | stockton, california, usa | 18 | 0195153448 | 0 | Classical Mythology | 2002 | Oxford University Press | http://images.amazon.com/images/P/0195153448.0... | http://images.amazon.com/images/P/0195153448.0... | http://images.amazon.com/images/P/0195153448.0...  | Provides an introduction to classical myths pl... | en | ['Social Science'] | stockton | california | usa  


Tabel 3. informasi singkat mengenai data  

| #  | Column       		| Non-Null Count | Dtype  |
| -- | -------------------- | -------------- | ------ |
| 0  | Unnamed: 0  			| 1031175  		 | int64  |
| 1  | user_id      		| 1031175  		 | int64  |
| 2  | location  			| 1031175  		 | object |
| 3  | age  				| 1031175  		 | float64|
| 4  | isbn  				| 1031175  		 | object |
| 5  | rating  				| 1031175  		 | int64  |
| 6  | book_title   		| 1031175  		 | object |
| 7  | book_author 			| 1031175  		 | object |
| 8  | year_of_publication  | 1031175  		 | float64|
| 9  | publisher 			|  1031175 		 | object |
| 10 | img_s				| 1031175  		 | object |
| 11 | img_m				| 1031175  		 | object |
| 12 | img_l				| 1031175  		 | object |
| 13 | Summary				| 1031175  		 | object |
| 14 | Language				| 1031175  		 | object |
| 15 | Category				| 1031175  		 | object |
| 16 | city					| 1017072  		 | object |
| 17 | state				| 1008377  		 | object |
| 18 | country 				| 995801   		 | object |

Tabel 4. Distribusi variabel rating

| rating | count |
|--------|-------|
|0       |647323 |
|1       |1481   |
|2       |2375   |
|3       |5118   |
|4       |7617   |
|5       |45355  |
|6       |31689  |
|7       |66404  |
|8       |91806  |
|9       |60780  |
|10      |71227  |

Dari tabel 2 dan 3, dapat dilihat ada beberapa kolom yang tidak akan digunakan dan akan lebih baik jika di hapus. Dari tabel 4 dapat dilihat bahwa 0 ada rating artinya pengguna pernah membaca buku, tetapi tidak memberikan rating, sehingga akan lebih baik jika rating 0 di hapus, menyisakan 1 s.d. 10.

## Data Preparation
***
### Langkah-langkah pra-pemrosesan data
1. Membaca _dataset_ menggunakan _pandas_
2. _Drop_ data kosong (_NaN_)
3. _Drop_ kolom yang tidak akan digunakan
4. _Drop_ nilai yang _invalid_ pada kolom

#### Membaca _dataset_
Pada bagian ini akan digunakan _library pandas_ untuk dapat membaca dan merubah _dataset_ menjadi _DataFrame_,  dari berkas yang diunduh akan ada 2 _file_, diproyek ini digunakan file dengan nama _Books Data with Category Language and Summary_ yang didalam file akan ditemukan berkas csv yang datanya sudah di proses terlebih dahulu. _Sample dari _dataset_ ini dapat dilihat pada tabel 2.

#### Drop data kosong
Pada bagian ini kita dapat melihat tabel 3 bahwa kolom `city, state, dan country` jumlahnya tidak sama dengan kolom lainnya. Untuk proyek ini, akan digunakan fungsi `dropna()`, dengan fungsi ini jika ada data kosong dalam bagian baris _DataFrame_ maka seluruh baris akan dihapus. Untuk melihat _count_ dari tiap kolom setelah dihapus dapat dilihat di tabel 5. 

Tabel 5. Informasi tentang data setelah _preprocess_

#### Drop kolom/nilai 

## Referensi
[[1]](https://media.neliti.com/media/publications/96720-ID-rumah-baca-jendela-dunia-sebuah-model-pe.pdf) Gresi A.R., Alan N., Khasanah B.R., Robby A.S., Priyadi N.P. (2013). Rumah Baca Jendela Dunia, Sebuah Model Perpustakaan Panti Asuhan. Jurnal Ilmiah Mahasiswa, Vol. 3 No.2. https://media.neliti.com/media/publications/96720-ID-rumah-baca-jendela-dunia-sebuah-model-pe.pdf
