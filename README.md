# Laporan Proyek Machine Learning - Optra Dananjaya


## 📌 Project Overview

Sistem rekomendasi merupakan bagian penting dari teknologi informasi modern, terutama dalam konteks big data dan personalisasi layanan digital. Dalam era digital yang ditandai dengan melimpahnya informasi, pengguna kerap merasa kewalahan saat memilih konten, seperti film, musik, atau produk. Oleh karena itu, sistem rekomendasi hadir sebagai solusi yang mampu memprediksi preferensi pengguna dan menyarankan konten yang relevan.

Khusus dalam industri film, sistem rekomendasi telah terbukti mampu meningkatkan kepuasan dan loyalitas pengguna. Platform seperti Netflix mencatat bahwa lebih dari 80% film yang ditonton berasal dari hasil rekomendasi sistem mereka [1]. Dengan kata lain, algoritma rekomendasi tidak hanya berfungsi sebagai alat bantu, tetapi juga menjadi pendorong utama engagement pengguna.

Dalam konteks akademik dan pengembangan teknologi di Indonesia, sistem rekomendasi juga menjadi topik yang banyak diteliti. Menurut penelitian oleh Nurhayati et al., sistem rekomendasi dapat meningkatkan efisiensi pencarian informasi dan memberikan nilai tambah dalam aplikasi digital berbasis pengguna [2]. Studi lain oleh Wibowo (2020) menyatakan bahwa pendekatan collaborative filtering dan content-based filtering adalah metode yang umum digunakan dalam pengembangan sistem rekomendasi di Indonesia [3].

Untuk proyek ini, digunakan dataset **MovieLens** dari GroupLens Research yang telah banyak digunakan dalam penelitian sistem rekomendasi. Dataset ini menyediakan informasi rating film dari pengguna, metadata film, serta timestamp yang dapat digunakan untuk mengembangkan dan mengevaluasi berbagai pendekatan sistem rekomendasi, baik berbasis konten maupun kolaboratif.

Proyek ini bertujuan untuk:
- Membangun sistem rekomendasi film yang personal dan relevan.
- Membantu pengguna menemukan film dengan lebih cepat dan sesuai minat.
- Memberikan pemahaman praktis tentang implementasi dan evaluasi sistem rekomendasi.

---

### Referensi

[1] G. Gomez-Uribe and N. Hunt, "The Netflix Recommender System: Algorithms, Business Value, and Innovation", *ACM Transactions on Management Information Systems (TMIS)*, vol. 6, no. 4, pp. 1–19, 2015. DOI: [10.1145/2843948](https://doi.org/10.1145/2843948)

[2] S. Nurhayati, D. Supriyadi, and M. Marwan, “Penerapan Sistem Rekomendasi dalam E-learning Menggunakan Metode Collaborative Filtering,” *Jurnal Teknologi dan Sistem Komputer*, vol. 6, no. 1, pp. 12–18, 2018. Available at: [https://jtsiskom.undip.ac.id/index.php/jtsiskom/article/view/292](https://jtsiskom.undip.ac.id/index.php/jtsiskom/article/view/292)

[3] H. Wibowo, “Penerapan Sistem Rekomendasi Film Menggunakan Metode Content-Based Filtering,” *Jurnal Teknologi Informasi dan Komunikasi*, vol. 9, no. 2, pp. 87–94, 2020. Available at: [https://jurnal.stmikjayakarta.ac.id/index.php/jtik/article/view/214](https://jurnal.stmikjayakarta.ac.id/index.php/jtik/article/view/214)

---


## 💼 Business Understanding

Sistem rekomendasi film bertujuan untuk memberikan pengalaman pengguna yang lebih baik dengan menyarankan film yang relevan berdasarkan preferensi dan histori pengguna. Dalam proyek ini, digunakan dataset MovieLens yang menyediakan data rating, metadata film, dan tag untuk membangun sistem rekomendasi yang adaptif.

### Problem Statements

- **Pernyataan Masalah 1**: Pengguna kesulitan menemukan film yang sesuai dengan preferensinya di antara ribuan pilihan yang tersedia.
- **Pernyataan Masalah 2**: Rekomendasi film yang diberikan secara umum (non-personal) cenderung tidak relevan dan mengurangi minat pengguna.
- **Pernyataan Masalah 3**: Sistem rekomendasi sederhana tidak dapat memanfaatkan pola kompleks yang tersembunyi dalam data pengguna dan konten film.

### Goals

- **Goal 1**: Mengembangkan sistem rekomendasi yang mampu menyarankan film sesuai minat pengguna berdasarkan data histori dan konten film.
- **Goal 2**: Meningkatkan relevansi dan personalisasi dalam sistem rekomendasi sehingga meningkatkan kepuasan pengguna.
- **Goal 3**: Mengimplementasikan pendekatan modern untuk menangkap hubungan non-linear dan interaksi pengguna dengan film.

---

### 🔍 Solution Statements

Untuk mencapai tujuan di atas, digunakan dua pendekatan sistem rekomendasi yang berbeda:

#### 1. **Content-Based Filtering**
- Menggunakan metadata film (seperti genre) dan teknik *TF-IDF* untuk merepresentasikan fitur teks.
- Menghitung kemiripan antar film menggunakan *cosine similarity*.
- Sistem menyarankan film yang mirip dengan yang disukai pengguna.

#### 2. **Neural Collaborative Filtering**
- Menggunakan arsitektur deep learning untuk mempelajari representasi vektor pengguna dan item (film).
- Memanfaatkan lapisan embedding, concatenation, dan dense layers untuk memodelkan interaksi kompleks antara pengguna dan film.
- Lebih fleksibel dibanding pendekatan klasik karena dapat menangkap pola non-linear dan implicit feedback.

Kombinasi dari kedua pendekatan ini diharapkan mampu menghasilkan sistem rekomendasi yang lebih akurat dan adaptif.

---

## 📊 Data Understanding

Dataset yang digunakan dalam proyek ini adalah **MovieLens Latest Small Dataset**, yang disediakan oleh [GroupLens Research](https://grouplens.org/datasets/movielens/). Dataset ini tersedia untuk umum dan dapat diunduh di tautan berikut: [https://files.grouplens.org/datasets/movielens/ml-latest-small.zip](https://files.grouplens.org/datasets/movielens/ml-latest-small.zip)

Dataset ini berisi data rating, metadata film, dan tag pengguna terhadap film. Secara keseluruhan, dataset ini terdiri dari empat file utama:

- `ratings.csv`: berisi informasi rating film dari pengguna.
- `movies.csv`: berisi metadata film seperti judul dan genre.
- `tags.csv`: berisi tag/kata kunci yang diberikan oleh pengguna ke film tertentu.
- `links.csv`: berisi ID referensi film ke database eksternal seperti IMDb dan TMDb.

Berikut penjelasan masing-masing variabel pada dataset:

### 🗂️ movies.csv
- `movieId`: ID unik untuk setiap film.
- `title`: Judul film beserta tahun rilis.
- `genres`: Genre film yang dipisahkan dengan tanda pipe (`|`), seperti `Action|Adventure|Comedy`.

### 🗂️ ratings.csv
- `userId`: ID pengguna yang memberikan rating.
- `movieId`: ID film yang diberi rating.
- `rating`: Nilai rating dari pengguna terhadap film, dalam skala 0.5 sampai 5.0.
- `timestamp`: Waktu rating diberikan dalam format UNIX time.

### 🗂️ tags.csv
- `userId`: ID pengguna yang memberikan tag.
- `movieId`: ID film yang diberi tag.
- `tag`: Kata kunci atau label yang diberikan ke film.
- `timestamp`: Waktu tag diberikan dalam format UNIX time.

### 🗂️ links.csv
- `movieId`: ID film di MovieLens.
- `imdbId`: ID film di IMDb.
- `tmdbId`: ID film di TMDb (The Movie Database).

---

### 🔍 Exploratory Data Analysis (EDA)

Beberapa langkah awal yang dilakukan untuk memahami data:

- **Distribusi rating** menunjukkan bahwa sebagian besar pengguna memberikan rating antara 3.0 hingga 4.5.
![Gambar distribusi rating](https://github.com/Optra123/Project-Recommendation-System-Dicoding/blob/main/image/distribution_rating.png?raw=true)

- **Genre populer** di dataset ini termasuk Drama, Comedy, dan Action.
![Gambar genre terpopuler](https://github.com/Optra123/Project-Recommendation-System-Dicoding/blob/main/image/genre_populer.png?raw=true)

- **Pola user-film** menunjukkan bahwa sebagian besar pengguna hanya menilai sebagian kecil dari total film, menunjukkan sifat sparsity yang umum dalam sistem rekomendasi.
![Gambar persebaran rating film](https://github.com/Optra123/Project-Recommendation-System-Dicoding/blob/main/image/jumlah_rating_film.png?raw=true)

Visualisasi dan pembersihan data akan dilakukan untuk memastikan kualitas dan konsistensi data sebelum masuk ke tahap pemodelan.

---

## 📊 Data Preparation

Setelah memahami karakteristik dataset MovieLens melalui tahap *Data Understanding*, langkah selanjutnya adalah mengolah dan menyusun data agar siap digunakan dalam proses pemodelan sistem rekomendasi. Tahap *Data Preparation* ini penting untuk memastikan bahwa model **Content-Based Filtering** dan **Collaborative Filtering** yang akan dibangun dapat memanfaatkan informasi yang tersedia secara optimal.

### ✨ Tujuan Data Preparation
Pada section ini, dilakukan dua proses utama:

1. **Penggabungan Fitur Film**  
   Informasi `genres` dan `tag` digabung menjadi satu fitur baru untuk menciptakan representasi film yang lebih komprehensif. Genre menunjukkan kategori film, sementara tag mengandung kata kunci yang diberikan oleh pengguna. Kombinasi keduanya memberikan konteks yang lebih kaya bagi sistem rekomendasi berbasis konten.

2. **Penanganan Missing Values**  
   Karena tidak semua film memiliki tag, kolom `tag` pada hasil penggabungan dapat berisi nilai kosong (NaN). Untuk menghindari error dalam pemrosesan lebih lanjut, semua nilai NaN diisi dengan string kosong (`''`).

### 🔧 Langkah-Langkah Teknis

```python
# Menggabungkan semua tag menjadi satu string per movieId, dipisahkan dengan koma
all_tags = tags.groupby('movieId')['tag'].apply(lambda tags: ', '.join(tags.astype(str))).reset_index()

# Menggabungkan dataset movies dengan tags yang telah digabung
movies_with_all_tags = pd.merge(movies, all_tags, on='movieId', how='left')

# Mengisi nilai NaN pada kolom 'tag' dengan string kosong
movies_with_all_tags['tag'] = movies_with_all_tags['tag'].fillna('')

# Membuat kolom baru 'combined_features' dengan menggabungkan genre dan tag
movies_with_all_tags['combined_features'] = movies_with_all_tags['genres'] + ', ' + movies_with_all_tags['tag']

# Menampilkan 5 baris pertama dari hasil akhir
movies_with_all_tags.head()
```

---

### 🧠 Alasan Diperlukannya Tahapan Ini
- Penggabungan fitur diperlukan agar model dapat menggunakan representasi teks yang mencerminkan baik kategori maupun deskripsi/tag dari film.

- Penanganan missing values penting untuk mencegah error saat pembuatan vektor fitur atau saat proses training model, khususnya dalam pemodelan berbasis teks seperti TF-IDF atau CountVectorizer.

---

## 🤖 Modeling

Setelah data film, rating, dan tag dipersiapkan pada tahap sebelumnya, kini masuk ke tahap utama yaitu membangun dan menguji sistem rekomendasi film. Dua pendekatan yang digunakan adalah **Content-Based Filtering** dan **Collaborative Filtering**. Masing-masing metode memiliki strategi yang berbeda dalam menyajikan rekomendasi yang relevan dan personal.

---

### 1️⃣ Content-Based Filtering

Content-Based Filtering memberikan rekomendasi berdasarkan kemiripan antar item (film), dalam hal ini berdasarkan **genre** dan **tag** yang telah digabung menjadi `combined_features`.

#### 🛠 Langkah-Langkah:

- Mengubah teks `combined_features` menjadi vektor numerik menggunakan **TF-IDF Vectorizer**.
- Mengukur kemiripan antar film menggunakan **Cosine Similarity**.
- Mengembangkan fungsi rekomendasi berdasarkan film yang dipilih pengguna.

#### ✅ Kelebihan:
- Tidak bergantung pada rating pengguna lain.
- Dapat memberikan rekomendasi bahkan untuk pengguna baru (cold-start user).

#### ❌ Kekurangan:
- Terbatas pada informasi konten yang tersedia.
- Tidak mempertimbangkan preferensi pengguna secara eksplisit.


### 2️⃣ Collaborative Filtering
Collaborative Filtering merekomendasikan film berdasarkan perilaku pengguna lain dengan preferensi serupa. Dalam implementasi ini digunakan pendekatan **matrix factorization** berbasis **embedding** dan model **deep learning** sederhana.

#### 🛠 Langkah-Langkah:
- Mengkodekan `userId` dan `movieId` ke dalam integer index.
- Membuat model neural network dengan lapisan embedding untuk user dan movie.
- Melatih model untuk memprediksi rating dan menghasilkan rekomendasi.

#### ✅ Kelebihan:
-Memahami preferensi pengguna berdasarkan pola interaksi historis.
-Bisa menangkap hubungan laten antara pengguna dan film.

#### ❌ Kekurangan:
-Rentan terhadap masalah cold-start (pengguna/film baru).
-Memerlukan data interaksi yang cukup banyak untuk hasil optimal.


### Output: Top-N Recommendations

#### 🎯 Content-Based Filtering

**Rekomendasi untuk film:** *Five Deadly Venoms (1978)*  
**Genre:** Action  
**Tag:** *(tidak tersedia)*  

| No. | Judul Film | Genre | Similarity Score |
|-----|------------|--------|------------------|
| 1   | Fair Game (1995) | Action | 1.0 |
| 2   | Under Siege 2: Dark Territory (1995) | Action | 1.0 |
| 3   | Hunted, The (1995) | Action | 1.0 |
| 4   | Bloodsport 2 (a.k.a. Bloodsport II: The Next Kumite) | Action | 1.0 |
| 5   | Best of the Best 3: No Turning Back (1995) | Action | 1.0 |
| 6   | Double Team (1997) | Action | 1.0 |
| 7   | Steel (1997) | Action | 1.0 |
| 8   | Knock Off (1998) | Action | 1.0 |
| 9   | Avalanche (1978) | Action | 1.0 |
| 10  | Aces: Iron Eagle III (1992) | Action | 1.0 |

**Precision:** `1.0`

---

#### 👥 Collaborative Filtering

**Rekomendasi untuk user:** `366`

**Top 3 Film dengan Rating Tertinggi oleh Pengguna:**

| No. | Judul Film | Genre | Rating |
|-----|------------|--------|--------|
| 1   | Reservoir Dogs (1992) | Crime \| Mystery \| Thriller | 5.0 |
| 2   | Interstellar (2014) | Sci-Fi \| IMAX | 5.0 |
| 3   | Fight Club (1999) | Action \| Crime \| Drama \| Thriller | 4.5 |

**Rekomendasi Film:**

| No. | Judul Film | Genre |
|-----|------------|--------|
| 1   | Shawshank Redemption, The (1994) | Crime \| Drama |
| 2   | Paths of Glory (1957) | Drama \| War |
| 3   | Ran (1985) | Drama \| War |
| 4   | Celebration, The (Festen) (1998) | Drama |
| 5   | Three Billboards Outside Ebbing, Missouri (2017) | Crime \| Drama |

---


## 🧪 Evaluation

Pada proyek ini, sistem rekomendasi dievaluasi dengan dua pendekatan utama: **Content-Based Filtering** dan **Collaborative Filtering**. Masing-masing menggunakan metrik evaluasi yang sesuai dengan karakteristik dan tujuan model.

### 🎯 Content-Based Filtering Evaluation

Untuk pendekatan Content-Based Filtering, metrik yang digunakan adalah **Precision**. Precision mengukur sejauh mana film-film yang direkomendasikan relevan dengan film yang menjadi acuan (input).

#### 📌 Formula Precision

Precision = (Jumlah Rekomendasi yang Relevan) / (Jumlah Total Rekomendasi)

Dalam konteks ini, suatu film dianggap relevan jika memiliki genre yang sama dengan film target.

#### 🧾 Hasil Evaluasi

Pengujian dilakukan dengan memilih film acak dari dataset, kemudian sistem memberikan 10 rekomendasi teratas. Berdasarkan hasil yang ditampilkan, seluruh rekomendasi memiliki genre yang sesuai, sehingga nilai **precision = 1.0**. Hal ini menunjukkan bahwa sistem berhasil merekomendasikan film yang secara konten sangat mirip dengan film acuan.

---

### 👥 Collaborative Filtering Evaluation

Untuk pendekatan Collaborative Filtering, digunakan **Mean Absolute Error (MAE)** sebagai metrik evaluasi. MAE digunakan untuk mengukur seberapa besar rata-rata kesalahan antara rating yang diprediksi oleh model dengan rating sebenarnya yang diberikan oleh pengguna.

#### 📌 Formula MAE

MAE = (1/n) × Σ |rating_aktual - rating_prediksi|

Keterangan:
- rating_aktual: rating asli yang diberikan oleh pengguna
- rating_prediksi: rating yang diprediksi oleh sistem
- n: jumlah data yang diuji

#### 🧾 Hasil Evaluasi

Model dilatih menggunakan teknik embedding dengan arsitektur neural network dan regularisasi L2. Proses pelatihan menunjukkan perbaikan performa dari waktu ke waktu. Hasil evaluasi divisualisasikan dengan grafik **Training MAE** dan **Validation MAE** selama proses training. Grafik tersebut menunjukkan tren penurunan error yang stabil, menandakan bahwa model cukup berhasil dalam mempelajari pola rating pengguna terhadap film.

---

### 🔍 Kesimpulan Evaluasi

- **Content-Based Filtering** menunjukkan hasil precision sempurna (1.0) pada pengujian tertentu, menandakan akurasi tinggi dalam hal kemiripan konten.
- **Collaborative Filtering** menunjukkan performa yang baik berdasarkan MAE, dengan nilai error yang menurun selama training, mengindikasikan model mampu mempelajari preferensi pengguna secara efektif.

Dengan demikian, kedua pendekatan memiliki kekuatan masing-masing, dan dapat digabungkan untuk membentuk sistem rekomendasi hybrid yang lebih akurat dan personal.



**---Ini adalah bagian akhir laporan---**

