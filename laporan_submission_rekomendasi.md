# Laporan Proyek Machine Learning - Nama Anda

## Project Overview

### Latar Belakang
Dalam era digital saat ini, perkembangan teknologi telah mengubah cara manusia mengakses dan mengosumsi hiburan, termasuk dalam hal menonton film. Dengan meningkatnya jumlah film yang dirilis setiap tahunnya, konsumen menghadapi tantangan dalam memilih film yang sesuai dengan preferensi mereka. Hal ini membuka peluang besar bagi pengembangan sistem rekomendasi berbasis data untuk membantu pengguna dalam menentukan film yang relevan. Maka dataset yang akan penulis analisis dan uji sistem pada rekomendasi film ialah **MovieLens**.

Dataset MovieLens menyajikan informasi tentang penilaian (rating) film yang diberikan oleh pengguna terhadap berbagai film. dataset ini telah digunakan secara luas dalam penelitian sistem rekomendasi karena kelengkapan dan kestabilannya dalam menyajikan hubungan antara pengguna dan item [1]. Melalui analisis lebih lanjut, penulis akan mengembangkan berbagai model prediksi seperti **Collaborative Filtering** dan **Content Based Filtering**.

Permasalahn utama yang ingin diselesaikan dalam proyek ini adalah **bagaimana memanfaatkan data historis dari penilaian pengguna** untuk membangun model prediktif yang mampu merekomendasikan film yang relevan bagi pengguna. Hal ini penting mengingat sistem rekomendasi pada peningkatan pengalaman pengguna, tetapi juga berdampak pada peningkatan keterlibaan dan keutungan platform layanan streaming[2]. menggunakan matrix factorization atau pendekatan deep learning seperti autoencoders yang efektif dalam menangkap pola preferensi pengguna[3]. maka dengan itu, penulis akan berfokus pada analisis dan pemodelan serta evaluasi model untuk mendapatkan hasil yang optimal.

### Referensi
[1] F. M. Harper and J. A. Konstan, “The MovieLens Datasets: History and Context,” ACM Transactions on Interactive Intelligent Systems (TiiS), vol. 5, no. 4, Article 19, Dec. 2015.

[2] X. Su and T. M. Khoshgoftaar, "A Survey of Collaborative Filtering Techniques," Advances in Artificial Intelligence, vol. 2009, Article ID 421425, 2009. doi:10.1155/2009/421425

[3] Y. Koren, R. Bell, and C. Volinsky, “Matrix Factorization Techniques for Recommender Systems,” IEEE Computer, vol. 42, no. 8, pp. 30–37, Aug. 2009. doi:10.1109/MC.2009.263

## Business Understanding

Pada tahap ini, penulis menjelaskan pemahaman-pemahaman dalam dataset yang akan di analisis lebih lanjut. sebagai berikut :     
  ### Problem Statment
- Mempelajari prefensi pengguna berdasarkan interaksi historis (rating).
- Membangun model yang mampu memberikan rekomendasi film yang relevan.
- Menentukan algoritma yang efektif untuk meningkatkan akurasi prediksi film yang diminati pengguna.

### Goals
- Menganalisis data MovieLens lebih lanjut untuk memahami pola perilaku pengguna terhadap film.
- Membuat perbandingan dengan beberapa model misalnya **Content-Based Filtering** dan **Collaborative Filtering**.
- Menggunakan **RMSE, Precesion, F-1 dan Recall** untuk mengevaluasi setiap model.

### Solusi Approach
setelah mendapatkan pernyataan masalah dan tujuan dalam MovieLens, maka penulis perlu mengatasi masalah yang diindetifikasi pada solusi approach. beberapa penjelesannya :  

**1. Content-Based-Filtering**

Pada model pertama yang akan penulis analisa lebih lanjut untuk menganlisis fitur dari rating seperti `genres`. Rekomendasi film akan diberikan berdasarkan kesamaan antara film yang sering diminati dan karakteristik yang sama.

Langkah-langkahnya ialah :

- Melakukan ekstraksi fitur konten dari fitur `genre`.
- Membuat representasi vector pada setiap film menggunakan TF-IDF.
- Menghitung kesamaan antar `genre` menggunakan **Cosine similarity**.
- Memberikan hasil rekomendasi berdasarkan film yang paling diminati.

**2. Collaborative Fitering**

Pada model kedua ini, Penulis melakukan suatu analisis lebih lanjut untuk memberikan rekomendasi berdasarkan kesamaan perilaku antar pengguna. pendekatan ini memanfaatkan fitur rating yang diberikan oleh pengguna terhadap film dan menemukan pola kemiripan antar pengguna atau genre.

Langkah-langkahnya ialah :    

- Menggunakan User-item-rating matrix dari data MoviLens.
- Menerapkan motode **User-Based** dan **Item-Based** pada Collaborative Filtering.
- Menggunakan **matrix factorization**.
- Memberikan hasil rekomendasi berdasarkan pola rating dari pengguna yang serupa.

## Data Understanding
Pada tahap ini,penulis akan menjelaskan informasi mengenai jumlah data, kondisi data, dan informasi mengenai data yang digunakan untuk analisis data sampa evaluasi model pada dataset yang kita analisis lebih lanjut.saya mengambil dataset dari platform **kaggle** yaitu dataset **MovieLens**

berikut link datasetnya : https://www.kaggle.com/datasets/snehal1409/movielens <br>
#### 1. Jumlah Variabel pada Dataset MovieLens 
Dataset ini terdiri 5 file yaitu :
- `rating.csv` : Berisi jumlah data rating yang diberikan pengguna pada film yang diminat/disukai oleh pengguna.
- `movie.csv` : berisi sejumlah data film/movie yang diminati pengguna sesuai genre yang pengguna sukai.
- `tag.csv` : berisi sejumlah tag pada film yang pengguna gemari.
- `link.csv` : berisi sejumlah link yang direkomendasikan pengguna ke pengguna lain sesuai minat gemar pengguna.
- `ReadMe.txt` : berisi informasi dataset `MovieLens`
#### 2. Informasi data setiap variabel
disini penulis akan menjelaskan informasi data dari setiap variabel dalam dataset `MovieLens` yaitu :
- **`movie.csv : `**  9125 entries dan 3 kolom.
- **`rating.csv :`** 1000004 entries dan 3 kolom.
- **`tag.csv :`** 1296 entries dan 4 kolom.
- **link.csv :`** 9125 entries dan 3 kolom.
#### 3. Penjelasan setiap variabel 
**A. movie.csv**<br>
- `movieId` memiliki jumlah Non-Null sebanyak 9125 entries dan type data ``int``.
- `title` memiliki jumlah Non-Null sebanyak 9125 entries dan type data ``object``.
- `genres` memiliki sejumlah Non-Null sebanyak 9125 entries dan type data ``object``.
**B. rating.csv**<br>
- `userId` memiliki sejumlah Non-Null sebanyak 100004 entries dan type data ``int``.
- `movieId` memiliki sejumlah Non-Null sebanyak 100004 entries dan typedata ``int``.
- `timpestamp` memiliki sejumlah Non-Null sebanyak 100004 entries dan typedata `int`.
**C. tag.csv** <br>
- `userId` memiliki sejumlah Non-Null sebanyak 1296 entries dan type data ``int``.
- `movieId` memiliki sejumlah Non-Null sebanyak 1296 entries dan type data ``int``.
- `tag` memiliki sejumlah Non-Null sebanyak 1296 entries dan type data ``object``.
- `timestamp` memiliki sejumlah Non-Null sebanyak 1296 entries dan type data `int`.
**D

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan. Sajikan top-N recommendation sebagai output.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menyajikan dua solusi rekomendasi dengan algoritma yang berbeda.
- Menjelaskan kelebihan dan kekurangan dari solusi/pendekatan yang dipilih.

## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
