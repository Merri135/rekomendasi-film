# Laporan Proyek Machine Learning - Merri Putri Panggabean

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
- Menggunakan metrik **RMSE,MSE Precesion@K dan Recall@K** untuk mengevaluasi setiap model.

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
Pada tahap ini,penulis akan menjelaskan informasi mengenai jumlah data, kondisi data, dan informasi mengenai data yang digunakan untuk analisis data sampai evaluasi model pada dataset yang penulis analisis lebih lanjut.penulis mengambil dataset dari platform **kaggle** yaitu dataset **MovieLens**

berikut link datasetnya : https://www.kaggle.com/datasets/snehal1409/movielens <br>
#### 1. Jumlah Variabel pada Dataset MovieLens 
Dataset ini terdiri 5 file yaitu :
- `rating.csv` : Berisi jumlah data rating yang diberikan pengguna pada film yang diminati/disukai oleh pengguna.
- `movie.csv` : berisi sejumlah data film/movie yang diminati pengguna sesuai genre yang pengguna sukai.
- `tag.csv` : berisi sejumlah tag pada film yang pengguna gemari.
- `link.csv` : berisi sejumlah link yang direkomendasikan pengguna ke pengguna lain sesuai minat gemar pengguna.
- `ReadMe.txt` : berisi informasi dataset `MovieLens`
#### 2. Informasi data setiap variabel
disini penulis akan menjelaskan informasi data dari setiap variabel dalam dataset `MovieLens` yaitu :
- **`movie.csv : `**  9125 entries dan 3 kolom.
- **`rating.csv :`** 1000004 entries dan 3 kolom.
- **`tag.csv :`** 1296 entries dan 4 kolom.
- **`link.csv :`** 9125 entries dan 3 kolom.
#### 3. Penjelasan setiap variabel 
**A. movie.csv<br>**
- `movieId` memiliki jumlah Non-Null sebanyak 9125 entries dan type data ``int``.
- `title` memiliki jumlah Non-Null sebanyak 9125 entries dan type data ``object``.
- `genres` memiliki sejumlah Non-Null sebanyak 9125 entries dan type data ``object``.<br>
berikut gambar hasil informasi variabel movie<br>
![alt text](./asset/movieinfo.png)<br>
Gambar 1. Informasi data variabel movie<br>

**B. rating.csv<br>**
- `userId` memiliki sejumlah Non-Null sebanyak 100004 entries dan type data ``int``.
- `movieId` memiliki sejumlah Non-Null sebanyak 100004 entries dan typedata ``int``.
- `timpestamp` memiliki sejumlah Non-Null sebanyak 100004 entries dan typedata `int`.<br>
berikut gambar hasil informasi variabel rating<br>
![alt text](./asset/ratinginfo.png)<br>
Gambar 2. Informasi data variabel rating<br>

**C. tag.csv<br>**
- `userId` memiliki sejumlah Non-Null sebanyak 1296 entries dan type data ``int``.
- `movieId` memiliki sejumlah Non-Null sebanyak 1296 entries dan type data ``int``.
- `tag` memiliki sejumlah Non-Null sebanyak 1296 entries dan type data ``object``.
- `timestamp` memiliki sejumlah Non-Null sebanyak 1296 entries dan type data `int`.<br>
berikut gambar hasil informasi variabel tag<br>
![alt text](./asset/taginfo.png)<br>
Gambar 3. Informasi data variabel tag<br>

**D. link.csv<br>**
- `movieId` memiliki sejumlah Non-Null sebanyak 9125 entries dan type data `int`.
- `imdbId` memiliki sejumlah Non-Null sebanyak 9125 entries dan type data `int`.
- `tmdbId` memiliki sejumlah Non-Null sebanyak 9125 entries dan type data `float`<br>
berikut gambar hasil informasi variabel link<br>
![alt text](./asset/linkinfo.png)<br>
Gambar 4. Informasi data variabel link<br>

#### 4. Ringkasan statistik data
**A. movie.csv<br>**
Beberapa insight pada variabel `movie`, diantaranya :<br>
- Jumlah data yang dimiliki pada variabel `movie` ialah 9125 data, rata-rata data ialah 31123 data, standar deviasi ialah 40782 data.
- dari yang penulis ketahui dari kolom `title` bahwa judul film yang sering muncul 2 kali ialah `Halmet (2000)` dan dari kolom `genre` yang banyak diminati pengguna ialah `drama`.<br>
berikut gambar hasil dari data statistik variabel movie<br>
![alt text](./asset/moviedescribe.png)<br>
Gambar 5. Data statistik variabel movie<br>

**B. rating.csv<br>**
beberapa insight pada variabel `rating` diantaranya :<br>
- Dataset berisi 100.004 rating dari berbagai user dan film, dengan distribusi waktu yang panjang (1990-an sampai 2016).
- Rating cenderung tinggi, menunjukkan potensi bias positif dari pengguna.
- pada variabel `rating` kolom `movieId` mengalami duplikat data yang akan di bersihkan pada tahap selanjutnya.<br>
berikut gambar hasil dari data statistik variabel rating<br>
![alt text](./asset/ratingdescribe.png)<br>
Gambar 6. Data statistik variabel rating<br>

**C. tag.csv<br>**
beberapa insight pada variabel `tag` diantaranya :<br>
- dataset pada variabel `tag` memiliki data sebanyak 1296 entries dari pengguna dan film.
- interaksi yang didapat bahwa film didominasi oleh film-film dengan userId yang relatif rendah dengan sejumlah kecil interaksi terjadi pada film-film dengan userId yang sangat tinggi.
- mayoritas interaksi didominasi dengan rentang waktu dari pertengahan tahun 2012 sampai tahun 2016.<br>
berikut gambar hasil data statistik variabel tag<br>
![alt text](./asset/tahdescribe.png)<br>
Gambar 7. Data statistik variabel tag<br>

**D. link.csv<br>**
beberapa insight yang didapat dari variabel `link` diantaranya :<br>
- terdapat rentang nilai yang sangat lebar, ditunjukkan perbedaan besar antara nilai `min` dan `max` serta `std` yang signifikan. Hal ini mengindikasikan bahwa dataset mencakup film-film dengan ID yang beragam dalam masing-masing sistem.<br>
berikut gambar hasil data statistik varaibel link<br>
![alt text](./asset/linkdescribe.png)<br>
Gambar 8. Data statistik variabel link<br>

#### 5. Informasi kondisi data
**A. Variabel movie<br>**
Pada variabel movie tidak memiliki missing value dan semua data pada `movie` memiliki **data bersih.<br>**
  
**B. Variabel rating<br>**
semua data dalam variabel `rating` tidak memiliki missing value dan user yang memberikan rating pada film cenderung tidak berstruktur dimana adanya user memberikan rating 1 sampai 4 pada film.<br>

**C. Variabel tag<br>**
semua data pada variabel `tag` tidak memiliki memiliki missing value.<br>

**D. Variabel link<br>**
pada semua data dalam variabel `link` tidak memiliki missing value.<br>

#### 6. Cek duplikat data
Pada tahap ini, penulis perlu untuk mengecek apakah setiap variabel memiliki data duplikat, dari pengujian yang penulis lakukan, bahwa **semua variabel tidak memiliki duplikat data<br>**.

### Exploratory Data Analysis (EDA)
**Distribusi Rating<br>**
![alt text](./asset/rating.png)<br>
Gambar 9. Distribusi Visualisasi Rating<br>
Pada hasil Visualisasi yang didapat bahwa distribusi condong kekanan (positif), mayoritas pengguna memberikan rating 3-5, tetapi rating terbanyak ialah rating 4 sebanyak 30.000 rating sedangkan rating 1 dan 2 memiliki jumlah yang sangat kecil dimana sedikit pengguna yang tidak menyukai film.<br>

**Distribusi Genre<br>**
![alt text](./asset/genre.png)<br>
Gambar 10. Distribusi Visualisasi Genre<br>
Pada hasil visualisasi yang diketahui bahwa genre drama yang paling banyak mencapai 4000 film diikuti oleh genre Comedy sebanyak 3000 film. sedangkan genre yang paling sedikit diminati ialah Horror, Sci-Fi,dan Fantasy sebanyak 1000 film.<br>

### Data Processing 
Pada tahap ini, penulis melakukan Processing dari semua dataset yang telah penulis lakukan sebelumnya di data understanding, sekarang penulis perlu untuk melakukan penggabungan dataset yang akan dianalisis lebih lanjut ke model yang akan penulis latih. langkah - langkah yang dilakukan penulis ialah :<br>
1. menggabungkan semua data movieId<br>
2. menggabungkan semua data userId<br>
3. menyimpan ke dataframe baru.<br>
4. mengecek missing value<br>
5. menampilkan hasil rating tertinggi dan terendah<br>


**1. Menggabungkan semua data movieId<br>**
  Pada tahap ini, penulis melakukan penggabungan data terhadap data unik `movieId` dari semua variabel-varibel yang memiliki hubungan satu sama lain, setelah melakukan penggabungan data unik, penulis menampilkan banyak jumlah data unik `movieId`. berikut jumlah data unik `movieId`<br>
![alt text](./asset/lost.png)<br>
Gambar 11. Hasil jumlah data `movieId`.<br>

**2. Menggabungkan semua data userId<br>**
Pada tahap ini, penulis melakukan penggabungan data terhadap data unik `userId` dari semua variabel-variabel yang memiliki hubungan satu sama lain, setelah melakukan penggabungan data unik, penulis menampilkan hasil jumlah dari penggabungan yang penulis buat, berikut hasilnya<br>
![alt text](./asset/unik.png)<br>
Gambar 12. Hasil jumlah data `userId`<br>

**3. Menyimpan ke dataframe baru<br>**
setelah melakukan penggabungan data unik sebelumnya, maka penulis perlu untuk menyimpan semua penggabungan data unik kedalam dataframe baru yaitu `all_movie_name`, seperti gambar berikut<br>
![alt text](./asset/user.png)<br>
Gambar 13. penggabungan kedua variabel<br> 

**4. Mengecek missing value<br>**
setelah melakukan tahap penggabungan dan menyimpan ke dataframe baru, maka penulis perlu untuk mengetahui apakah data memiliki missing value, dari yang penulis ketahui bahwa `all_movie_name`` tidak memiliki nilai kosong berikut hasilnya<br>
![alt text](./asset/missing.png)<br>
Gambar 14. Missing value<br>

**5. Menampilkan hasil rating tertinggi dan terendah<br>**
Pada tahap ini, penulis melakukan untuk menampilkan hasil penggabungan pada rating tertinggi dan terendah berdasarkan judul film, dari penulis yang ketahui bahwa rating tertinggi pada judul fiml ialah **Zerophilia (2005) sampai Drained (O cheiro do Ralo) (2006)** memiliki rating dengan 5.0. dan rating terendah pada judul film adalah **Zombie Holocaust (a.k.a. Doctor Butcher M.D.) (Zombi Holocaust) (1980) sampai Santa with Muscies (1996)** memiliki rating terendah dengan rating 0.5 . berikut hasilnya<br>
![alt text](./asset/tinggi.png)<br>
Gambar 15. Hasil Rating tertinggi<br>

![alt text](./asset/rendah.png)<br>
Gambar 16. Hasil Rating terendah<br>

## Data Preparation
Pada tahap ini, penulis melakukan data preparation pada semua data yang telah penulis lakukan pada tahap sebelumnya. berikut langkah-langkah tahap preparation yang akan dilakukan:<br>
1. Konversi kolom `timestamp` ke type data **datetime**.<br>
2. menghapus duplikat data.<br>
3. Konversi semua series ke `list`.<br>
4. memasukkan ke Dictionary baru.<br>

**1. Konversi kolom **``Timestamp``**<br>**
Pada tahap ini, penulis perlu untuk melakukan konversi data type data `timestamp` menjadi typedata **datetime.<br>**

**2. Menghapus duplikat data<br>**
Pada tahap ini, penulis melakukan hapus duplikat data menggunakan fungsi `.drop_duplikat` pada dataset.<br>

**3. Konversi semua series ke list<br>**
Pada tahap ini, penulis melakukan konversi semua data series `movie` kedalam bentuk **list.** berfungsi untuk mengembalikan representasi array dalam bentuk list pada dataset.<br>

**4. Memasukkan data ke Dictionary baru<br>**
Pada tahap ini, penulis melakukan penyimpanan data yang telah diubah dan diberihkan ke dalam dict baru yaitu `movie_new`.<br>

## Modeling
Pada tahap ini, penulis menggunakan 2 model yang berbeda yaitu :<br>
**1. Content-Based Filtering<br>**
**2. Collaborative Filtering<br>**

#### 1. Content-Based Filtering
Pada model ini bertujuan untuk merekomendasikan item berdasarkan **kemiripan atribut konten** antara item yang sering disukai pengguna dengan item lainnya.<br>

**Cara kerjanya sebagai berikut :<br>**
- **melakukan ekstraksi fitur** : pada tahap ini, model mengambil item yang akan di representasikan fitur kedalam bentuk vector dengan menggunakan **TF-IDF dan encoded** pada fitur.
- **menghitung kemiripan(similarity)** : Pada tahap ini, model mengukur kemiripan dari pengguna dan semua item yang tersedia dengan menggunakan metrik **Cosine Similarity** pada fitur yang akan dianalisis lebih lanjut serta memberikan hasil fitur yang sesuai.
- **menyajikan hasil rekomendasi** : Pada tahap ini, model menampilkan hasil yang telah diurutkan berdasarkan skor kemiripan tertinggi.<br>

**Kelebihan dan kekurangan Content-Based Filtering<br>**
- **Kelebihan** pada model ini ialah tidak bergantung pada interaksi pengguna lain dan efektif untuk pengguna baru yang memiliki preferensi awal atau cocok untuk **user cold-start**
- pada model ini juga memiliki **kekurangan** ialah model terbatas pada konten yang mirip dengan yang sudah disukai dan tidak bisa merekomendasi item yang tidak punya metadata yang lengkap.

**Output :<br>**
berikut 2 nilai input film pada model **Content-Based Filtering**<br>
![alt text](./asset/toy.png)<br>
![alt text](./asset/jumanji.png)<br>
Gambar 17. Hasil Output Content Based Filtering<br>
dari gambar diatas, penulis menampilkan 2 contoh judul film yang penulis rekomendasikan untuk melihat seberapa banyak pengguna menyukai film tersebut, dari yang penulis ketahui bahwa film **Toy Story (1995) dan Jumanji (1995)** memiliki 10 top yang banyak diminati oleh pengguna. berikut hasilnya<br>

- **Toy Story (1995)<br>**
![alt text](./asset/toys.png)<br>
- **Jumanji (1995)<br>**
![alt text](./asset/jumanjis.png)<br>
Gambar 18. Hasil 10 Top yang diminati pengguna<br>

#### 2. Collaborative Filtering
Pada tahap ini, penulis menggunakan model kedua yaitu **Colaborative Filtering** menggunakan *Tensorflow Keras* untuk melakukan rekomendasi item berdasarkan **interaksi pengguna lain** yang memiliki preferensi yang mirip.<br>

**Cara kerjanya sebagai berikut :<br>**
- **membangun matriks interaksi** : Pada tahap ini, model membuat matriks pengguna vs item. yang dimana berisi nilai interaksi jumlah film yang banyak diminati pengguna berdasarkan **rating**.
- **menghitung kemiripan** : Pada tahap ini,model melakukan kemiripan pada **user-based** dan **item-based** berdasarkan pola pengguna yang menyukai keduanya.
- **melakukan prediksi preferensi** : Pada tahap ini,model melakukan prediksi untuk item yang belum dilihat pengguna berdasarkan interaksi pengguna yang sama.
- **menyajikan hasil rekomendasi** : Pada tahap ini, model mengurutkan item berdasarkan skor prediksi yang telah dilatih dan mengambil hasil output untuk direkomendasikan.<br>

**Kelebihan dan kekurangan Collaborative Filtering<br>**
- **kelebihan** dari model ini ialah dapat direkomendasikan item berbagai genre dan tidak memerlukan detail konten item.
- tetapi **kekurangan** pada model ini adalah mudah terpengaruh pada masalah **cold-start** dan rentan terhadap **sparsity/sedikit interaksi pengguna.**
  
**Output :<br>**
dari hasil yang didapat dari model ini ialah banyak user yang memberikan rekomendasi pada film berdasarkan rating ialah :<br>
> userId : 30

![alt text](./asset/users.png)<br>
Gambar 19. Hasil jumlah users<br>
berikut hasil 10 top dari model 2: **Collaborative Filtering<br>**
![alt text](./asset/rekom.png)<br>
Gambar 20. 10 top rekomendasi film berdasarkan rating<br>
dari gambar yang diketahui bahwa genre yang paling banyak diminati oleh pengguna ialah **Drama**.<br>

#### Rekomendasi Top-N Film
- **Content-Based Filtering**: Berdasarkan kemiripan judul film.
- **Model-Based Collaborative Filtering**: Berdasarkan representasi hasil user dari jumlah rating.
  
## Evaluation
Pada tahap ini, penulis melakukan evaluasi kinerja sistem rekomendasi yang telah dilatih sebelumnya dengan menggunakan kedua model yaitu **Content-based filtering dan Colaborrative filtering**. berikut langkah-langkah kerjanya :<br>

#### 1. Content-Based Filtering
**Metriks Evaluasi**
Berikut metriks evaluasi yang akan digunakan untuk mengukur kinerja sistem rekomendasi film, sebagai berikut:<br>
A. Precision@5
B. Recall@5

**A. Precision@K5<br>**
Precision@5 mengukur proporsi item yang benar-benar relevan di antara K item teratas yang direkomendasikan oleh sistem. Precision@5 berguna untuk menampilkan hasil precision tertinggi yang paling relevan untuk diberikan ke pengguna.berikut rumus matriks *Precision@5* :<br>
![alt text](./asset/pre.png)<br>
Gambar 21. Rumus Precision@5<br>

- Recommended nilai K: Item yang direkomendasikan (top-K)
- cara kerja precision : *Precision@5* bekerja dengan menghitung berapa banyak film yang relevan diantara film yang direkomendasikan oleh sistem.sebagai contoh, jika nilai K diatur ke 10 maka akan menampilkan hasil persentase film yang relevan dengan 10 top teratas.

**B. Recall@5<br>**
Recall@5 mengukur proporsi item relevan yang berhasil ditemukan dalam top-K rekomendasi. Recall@5 berguna untuk memastikan bahwa film yang relevan tidak terlewatkan oleh sistem. berikut rumus metrik *Recall@5*:<br>
![alt text](./asset/rec.png)<br>
Gambar 22. Rumus metrik Recall@5.<br>

- Recommended K : Top-K item yang direkomendasikan yang paling relevan
- cara kerja Recall@5 : *Recall@5* bekerja untuk menghitung nilai top-K yang direkomendasikan untuk user sesuai total item yang paling relevan. contohnya, jika film **Toy Story (1995) dan Jumanji (1995)** direkomendasikan ke 10 top film terbaik, maka *Recall@5* akan memberikan hasil rekomendasi film yang paling relevan untuk user.<br>

#### Hasil Evaluasi
Berdasarkan hasil evaluasi yang didapatkan, berikut adalah peforma sistem rekomendasi pada dua film input yang penulis buat yaitu *"Toy Story (1995) dan Jumanji (1995)* :

- **Toy Story (1995) :**
  - *Precision@5* : 16,60%
  - *Recall@5* : 100,00%

untuk hasil pada film **Toy Story (1995)** memiliki *Precision@5* sebanyak 16,60% menunjukkan bahwa dari 5 film yang direkomedasikan untuk user yang paling relevan sebanyak 0,83% menandakan sistem berhasil menemukan item yang relevan untuk user. jika berdasarkan metriks *Recall@5* memiliki nilai sebanyak 100,00% menunjukkan semua film relevan berhasil ter-cover dalam 5 rekomendasi serta berhasil menemukan semua film yang penting dari daftar rekomendasi.

- **Jumanji (1995)**
  - *Precision@5* : 2,62%
  - *Recall@5* : 100,00%

untuk hasil yang didapat dari rekomendasi film yang kedua ialah bahwa nilai *Precision@5* sebanyak 2,62% yang menandakan bahwa model tidak memberikan rekomendasi film yang secara ketat relevan diantara 5 top rekomendasi. sedangkan dari metrik *Recall@5* memiliki nilai 100,00% yang menandakan bahwa model berhasil menangkap seluruh film yang relevan yang cocok dengan film **Jumanji (1995)** dalam *Cosine Similarity*.

### 2. Collaborative Filtering
**Metrik Evaluasi<br>**
Pada tahap ini, penulis melakukan evaluasi pada model **Collaborative Filtering** dengan menggunakan :<br>
1. RMSE
2. MSE

**1. Root Mean Squared Error (RMSE)<br>**
RMSE adalah akar kuadrat dari MSE yang berfungsi untuk mengukur perbedaan antara nilai rating asli dengan nilai rating yang diprediksi oleh model. berikut rumus RMSE :<br>
![alt text](./asset/rmse.png)<br>
Gambar 23. Rumus RMSE<br>
keterangan :<br>
N = Jumlah data<br>
^ yi : Nilai prediksi.<br>
yi = Nilai aktual (real).<br>

cara kerja pada metrik RMSE adalah RMSE memberikan gambaran seberapa jauh, rata-rata dan prediksi model dari nilai rating sebenarnya. jika nilai RMSE memiliki nilai rendah maka menunjukkan bahwa model lebih akurat dalam memprediksi rating. berikut hasil RMSE dari model <br>
![alt text](./asset/hasilrmse.png)<br>
Gambar 24. Hasil nilai erros RMSE<br>
dari yang penulis ketahui bahwa rata-rata kesalahan prediksi memiliki nilai cukup rendah yang mengindikasikan bahwa model memiliki peforma yang baik dengan skala 0-1.<br>

**2. Mean Absolute Error (MAE)<br>**
Pada tahap ini, penulis melakukan untuk memprediksi model menggunakan metrik MSE dengan menggunakan rumus sebagai berikut <br>
![alt text](./asset/mse.png)<br>
Gambar 25. Rumus MAE<br>
keterangan :<br>
N = Jumlah data<br>
^ yi : Nilai prediksi.<br>
yi = Nilai aktual (real).<br>

MAE mengukur rata-rata dari kuadrat selisih antara nilai prediksi dan nilai aktual. ini menunjukkan seberapa jauh prediksi model dari kenyataan tanpa memperhatikan arah. dengan menggunakan rumus MAE penulis mengetahui hasil nilai error terhadap model yang diuji. berikut hasilnya <br>
![alt text](./asset/hasilmse.png)<br>
Gambar 26. Hasil nilai error MAE<br>
dari gambar yang penulis ketahui bahwa nilai prediksi pada model memberikan prediksi rating yang cukup akurat dan lebih mudah diinterpretasikan dan kurang terpengaruh pada outlier.<br>

### Visualisasi Learning Curve 
setelah penulis mendapatkan hasil nilai error dari kedua metrik yang uji pada model, maka penulis perlu untuk menampilkan hasil evaluasi model yang telah diuji sebelumnya dengan menampilkan menggunakan learning curva. berikut tampilannya <br>
![alt text](./asset/curve.png)<br>
Gambar 27. Visualisasi Hasil Evaluasi<br>
dari gambar visualisasi hasil evaluasi yang penulis dapatkan menujukkan bahwa nilai data train terus menurun dengan bertambahnya epoch menandakan model belajar dengan baik dari data pelatihan, sedangkan pada data validation menurun dari awal tetapi stagnan bahkan sedikit naik di beberapa titik yang menandakan model mengalami indikasi overfitting dapat dilihat dari epoch ke-5 sampai epoch ke -6.<br>
 
### Kesimpulan 
- **Content-Based Filtering** hampir sama dengan analisis sentimen dimana sebagai pendekatan awal namun performa dalam memberikan rekomendasi pada user terbatas karena hanya mengandalkan judul film berdasarkan fitur **genre**. hasil evaluasi model yang didapat dengan menggunakan *Precision@5 dan Recall@5* memberikan nilai yang akurat serta memberikan rekomendasi film yang relevan untuk pengguna. dari 2 contoh film input yang di evaluasi yaitu **``Toy Story (1995) dan Jumanji (1995)``** mendapatkan hasil sebagai berikut <br>

| Film               | Precision@5 | Recall@5 |
|--------------------|-------------|----------|
| Toy Story (1995)   | 16.60%      | 100.00%  |
| Jumanji (1995)     | 2.62%       | 100.00%  |

<br>

- **Collaborative Filtering** memberikan hasil evaluasi dengan hasil terbaik serta performa yang baik dalam menangkap pola laten preferensi pengguna, dengan menggunakan 2 metrik pada model yaitu **RMSE dan MAE** yang menujukkan nilai error yang rendah dan performa yang baik pada model.
