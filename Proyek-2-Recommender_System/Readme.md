# Laporan Proyek Machine Learning 
***
## Project Overview

Buku adalah jendela dunia. Dengan membaca buku seseorang dapat memperoleh ilmu yang tiada batas, tanpa ada batasan waktu, dan mengenal seseorang dari seluruh sisi dunia, karena buku merupakan sumber ilmu pengetahuan. Untuk dapat memperoleh ilmu yang ada di dalam buku, seseorang harus membaca buku.[1] Kegiatan membaca buku ini sangat penting bagi manusia, dengan terbiasa membaca buku, maka seseorang akan memiliki pengetahuan yang luas. Namun dengan banyaknya jumlah buku yang tersedia terkadang membuat pembaca kebingungan dalam menentukan buku yang akan dibaca. Ada pula pembaca yang hanya ingin membaca buku yang mirip dengan yang pernah dibaca sebelumnya. Tidak jarang juga ditemui pembaca yang menentukan buku-buku yang akan dibaca selanjutnya berdasarkan penerbitnya, alasan dipilihnya penerbit dikarenakan tiap penerbit memiliki standar yang berbeda, sehingga banyak pembaca yang lebih suka dengan standar dari penerbit tertentu.

Berdasarkan permasalahan tersebut, pada proyek ini akan dibuat suatu model sistem rekomendasi menggunkaan _content-based filtering_ untuk merekomendasikan buku-buku yang mungkin akan dibaca oleh pengguna. _Content-based filtering_ merupakan metode yang digunakan untuk merekomendasikan _item_ berdasarkan "fitur" dari _item_ berdasarkan dari aksi atau _explicit feedback_ sebelumnya. Contohnya yaitu merekomendasikan suatu film berdasarkan tokoh utamanya. Dengan adanya sistem rekomendasi ini diharapkan dapat membantu pembaca untuk menentukan buku yang akan dibaca selanjutnya.

## Business Understanding
***
### Problem Statements
Berdasarkan penjelasan pada _project overview_, berikut merupakan rincian masalah yang perlu diselesaikan di proyek ini:
- Sistem rekomendasi apa yang baik diterapkan pada kasus ini?
- Bagaimana cara membuat sistem rekomendasi buku yang akan merekomendasikan buku berdasarkan fitur penerbit?

### Goals
Tujuan dibuatnya proyek ini adalah sebagai berikut:
- Membuat sistem rekomendasi buku dengan preferensi penerbit.
- Memberikan rekomendasi buku yang mungkin disukai pengguna.

### Solution Approach
Solusi yang dapat dilakukan untuk memenuhi tujuan dari proyek ini diantaranya:
-  Pra-pemrosesan data. Pada tahap ini dapat dilakukan beberapa tahapan, antara lain:
  - Penghapusan beberapa fitur yang tidak akan digunakan.
  - Memperbaiki nilai yang invalid/salah pada _dataset_.
  - Mengganti tipe data dari fitur.
  - Membuang nilai yang kosong.
- Persiapan data. Pada tahap ini dapat dilakukan beberapa tahapan, antara lain:
  - Menggabungkan _dataset_
  
  TBA*
  
 

## Referensi
[[1]](https://media.neliti.com/media/publications/96720-ID-rumah-baca-jendela-dunia-sebuah-model-pe.pdf) Gresi A.R., Alan N., Khasanah B.R., Robby A.S., Priyadi N.P. (2013). Rumah Baca Jendela Dunia, Sebuah Model Perpustakaan Panti Asuhan. Jurnal Ilmiah Mahasiswa, Vol. 3 No.2. https://media.neliti.com/media/publications/96720-ID-rumah-baca-jendela-dunia-sebuah-model-pe.pdf
