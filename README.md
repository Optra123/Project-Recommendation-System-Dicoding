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

### 📁 1. `ratings.csv`

**Jumlah Data:** 100836 baris, 4 kolom  
**Kondisi Data:** Tidak terdapat missing value, duplikat sudah dibersihkan.

**Deskripsi Fitur:**
- `userId`: ID pengguna yang memberikan rating.
- `movieId`: ID film yang diberi rating.
- `rating`: Nilai rating dari pengguna terhadap film (skala 0.5 sampai 5.0).
- `timestamp`: Waktu rating diberikan (UNIX time).

---

### 📁 2. `movies.csv`

**Jumlah Data:** 9742 baris, 3 kolom  
**Kondisi Data:** Tidak terdapat missing value, data cukup bersih.

**Deskripsi Fitur:**
- `movieId`: ID unik untuk setiap film.
- `title`: Judul film beserta tahun rilis.
- `genres`: Genre film yang dipisahkan dengan tanda pipe (`|`), misal `Action|Comedy`.

---

### 📁 3. `tags.csv`

**Jumlah Data:** 3683 baris, 4 kolom  
**Kondisi Data:** Tidak terdapat missing value, data bersifat subjektif dari pengguna.

**Deskripsi Fitur:**
- `userId`: ID pengguna yang memberikan tag.
- `movieId`: ID film yang diberi tag.
- `tag`: Kata kunci atau label yang diberikan ke film.
- `timestamp`: Waktu tag diberikan (UNIX time).

---

### 📁 4. `links.csv`

**Jumlah Data:** 9742 baris, 3 kolom  
**Kondisi Data:** Terdapat 8 nilai null pada kolom `tmdbId` (9734/9742 non-null).

**Deskripsi Fitur:**
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

Setelah memahami karakteristik dataset MovieLens melalui tahap *Data Understanding*, langkah selanjutnya adalah mempersiapkan data agar siap digunakan dalam proses pemodelan sistem rekomendasi. Tahap *Data Preparation* ini penting untuk memastikan bahwa model **Content-Based Filtering** dan **Collaborative Filtering** dapat bekerja secara optimal.

---

### ✨ Tujuan Data Preparation

Pada tahap ini dilakukan beberapa proses penting, yaitu:

1. **Penggabungan Fitur Film**  
   Informasi `genres` dan `tag` digabungkan untuk membentuk fitur baru bernama `combined_features`. Genre mencerminkan kategori film, sedangkan tag merupakan kata kunci yang diberikan pengguna. Kombinasi keduanya memberikan representasi yang lebih kaya bagi model Content-Based Filtering.

2. **Penanganan Nilai Kosong (Missing Values)**  
   Beberapa film tidak memiliki tag, sehingga nilai pada kolom `tag` bisa kosong. Untuk mencegah error, nilai NaN diubah menjadi string kosong (`''`).

3. **Ekstraksi Fitur dengan TF-IDF (Term Frequency-Inverse Document Frequency)**  
   Setelah fitur teks `combined_features` terbentuk, dilakukan proses ekstraksi vektor fitur menggunakan metode TF-IDF. Teknik ini digunakan untuk mengukur pentingnya sebuah kata dalam dokumen relatif terhadap keseluruhan dokumen, dan hasilnya digunakan sebagai representasi vektor untuk setiap film dalam model Content-Based Filtering.

4. **Persiapan Data untuk Collaborative Filtering**  
   Untuk model Collaborative Filtering, dipersiapkan matriks interaksi pengguna dan item (user-item interaction matrix). Dataset `ratings.csv` digunakan dengan melakukan pemetaan ulang data user dan item menjadi format numerik, lalu digunakan sebagai input model rekomendasi berbasis interaksi.

---

### 🔧 Langkah-Langkah Teknis

#### Penggabungan Fitur Film

```python
# Menggabungkan semua tag menjadi satu string per movieId
all_tags = tags.groupby('movieId')['tag'].apply(lambda tags: ', '.join(tags.astype(str))).reset_index()

# Menggabungkan dataset movies dengan tags
movies_with_all_tags = pd.merge(movies, all_tags, on='movieId', how='left')

# Menangani nilai NaN
movies_with_all_tags['tag'] = movies_with_all_tags['tag'].fillna('')

# Membuat fitur gabungan genres dan tag
movies_with_all_tags['combined_features'] = movies_with_all_tags['genres'] + ', ' + movies_with_all_tags['tag']
```

#### Ekstraksi Fitur TF-IDF
```python
# Membuat objek TF-IDF Vectorizer
tfidf = TfidfVectorizer(stop_words='english')

# Transformasi fitur gabungan menjadi vektor TF-IDF
tfidf_matrix = tfidf.fit_transform(movies_with_all_tags['combined_features'])
```

---

### 🧠 Alasan Diperlukan Tahapan Ini
- Penggabungan fitur memungkinkan sistem memahami lebih banyak informasi tentang film berdasarkan genre dan tag.

- Penanganan missing values mencegah error saat proses ekstraksi fitur teks.

- TF-IDF memberikan bobot pada kata berdasarkan seberapa penting kata tersebut dalam koleksi film — membantu sistem membedakan konten film secara tekstual.

- Label Encoding dan pembentukan matriks interaksi penting untuk mengubah data ke format numerik yang diperlukan oleh algoritma Collaborative Filtering.

---

## 🤖 Modeling

Pada tahap ini, dibangun dua pendekatan sistem rekomendasi: **Content-Based Filtering** dan **Collaborative Filtering**. Masing-masing pendekatan memiliki cara kerja dan keunggulan tersendiri dalam menghasilkan rekomendasi film yang relevan.

---

### 1️⃣ Content-Based Filtering

Content-Based Filtering bekerja dengan membandingkan kemiripan antar item (dalam hal ini, film). Sistem ini memberikan rekomendasi berdasarkan fitur konten film, seperti `genre` dan `tag`, tanpa memperhatikan preferensi pengguna lain.

#### 🔍 Cara Kerja:
1. **Representasi Teks:**  
   Setiap film direpresentasikan sebagai sebuah dokumen teks hasil penggabungan fitur `genres` dan `tag`.  
2. **Ekstraksi Fitur:**  
   Digunakan metode **TF-IDF Vectorizer** untuk mengubah dokumen teks menjadi representasi numerik berbasis bobot kata. TF-IDF membantu memberi nilai tinggi pada kata yang unik dan informatif dalam konteks kumpulan dokumen.  
3. **Menghitung Kemiripan:**  
   Digunakan **Cosine Similarity** untuk mengukur kesamaan antar film berdasarkan vektor TF-IDF-nya.  
4. **Rekomendasi Film:**  
   Diberikan film input, sistem menampilkan daftar film dengan skor kemiripan tertinggi.

#### ✅ Kelebihan:
- Dapat memberikan rekomendasi meskipun pengguna belum pernah memberikan rating (mengatasi cold-start pada user).
- Tidak memerlukan data interaksi antar pengguna.

#### ❌ Kekurangan:
- Rekomendasi terbatas pada fitur yang tersedia di film.
- Tidak mempertimbangkan preferensi atau kebiasaan pengguna secara eksplisit.

---

### 2️⃣ Collaborative Filtering

Collaborative Filtering memanfaatkan informasi dari interaksi pengguna terhadap film, seperti rating, untuk menyarankan item yang disukai oleh pengguna lain dengan perilaku serupa. Pendekatan ini sangat efektif karena dapat menangkap pola ketertarikan pengguna secara tidak langsung.

#### 🔍 Cara Kerja:
1. **Matriks Interaksi:**  
   Data rating pengguna diubah menjadi matriks interaksi pengguna-film.
2. **Encoding ID:**  
   `userId` dan `movieId` dikodekan ke indeks numerik menggunakan LabelEncoder.
3. **Model Embedding:**  
   Dibuat model neural network sederhana menggunakan dua layer **embedding** — satu untuk pengguna dan satu untuk film. Embedding ini bertugas memetakan user dan item ke dalam vektor berdimensi rendah.
4. **Prediksi Rating:**  
   Vektor embedding pengguna dan film dikombinasikan melalui operasi dot product untuk menghasilkan prediksi rating.
5. **Rekomendasi Film:**  
   Model dilatih untuk meminimalkan selisih antara prediksi dan rating asli. Setelah itu, sistem memberikan rekomendasi film dengan rating tertinggi yang belum pernah ditonton oleh pengguna.

#### ✅ Kelebihan:
- Menyesuaikan rekomendasi berdasarkan preferensi pengguna.
- Dapat menangkap relasi laten antara pengguna dan item yang tidak terlihat dari data eksplisit.

#### ❌ Kekurangan:
- Membutuhkan data interaksi yang cukup banyak.
- Tidak dapat merekomendasikan item baru yang belum pernah dirating oleh pengguna mana pun (item cold-start).

---

### 🎯 Hasil Rekomendasi

#### 📌 Content-Based Filtering

**Rekomendasi berdasarkan film input:** *Five Deadly Venoms (1978)*

| No. | Judul Film                                                   | Genre   | Similarity Score |
|-----|--------------------------------------------------------------|---------|------------------|
| 1   | Fair Game (1995)                                             | Action  | 1.0              |
| 2   | Under Siege 2: Dark Territory (1995)                         | Action  | 1.0              |
| 3   | Hunted, The (1995)                                           | Action  | 1.0              |
| 4   | Bloodsport 2 (a.k.a. Bloodsport II: The Next Kumite)        | Action  | 1.0              |
| 5   | Best of the Best 3: No Turning Back (1995)                  | Action  | 1.0              |

**Precision:** `1.0`

---

#### 👤 Collaborative Filtering

**Contoh pengguna:** `User 366`

**Film dengan rating tertinggi oleh user:**

| No. | Judul Film                      | Genre                              | Rating |
|-----|--------------------------------|-------------------------------------|--------|
| 1   | Reservoir Dogs (1992)          | Crime \| Mystery \| Thriller        | 5.0    |
| 2   | Interstellar (2014)            | Sci-Fi \| IMAX                      | 5.0    |
| 3   | Fight Club (1999)              | Action \| Crime \| Drama \| Thriller| 4.5    |

**Rekomendasi Film Berdasarkan Model:**

| No. | Judul Film                                    | Genre             |
|-----|-----------------------------------------------|-------------------|
| 1   | Shawshank Redemption, The (1994)              | Crime \| Drama    |
| 2   | Paths of Glory (1957)                         | Drama \| War      |
| 3   | Ran (1985)                                    | Drama \| War      |
| 4   | Celebration, The (Festen) (1998)              | Drama             |
| 5   | Three Billboards Outside Ebbing, Missouri (2017) | Crime \| Drama |

---

### 🧠 Kesimpulan Sementara

Dua pendekatan yang digunakan memiliki karakteristik berbeda dan dapat saling melengkapi. Content-Based Filtering cocok untuk memberikan rekomendasi berbasis konten film yang telah dikenal, sedangkan Collaborative Filtering lebih efektif untuk mempersonalisasi rekomendasi berdasarkan pola perilaku pengguna.

---


## 🧪 Evaluation

Tahap evaluasi bertujuan untuk mengukur performa dari dua pendekatan sistem rekomendasi yang dikembangkan, yaitu **Content-Based Filtering** dan **Collaborative Filtering**, serta menilai sejauh mana solusi yang diterapkan menjawab kebutuhan pengguna dan tujuan bisnis yang telah ditetapkan.

---

### 🎯 Content-Based Filtering Evaluation

Untuk pendekatan Content-Based Filtering, evaluasi dilakukan menggunakan metrik **Precision**, karena sistem merekomendasikan daftar film yang mirip dengan satu film input. 

#### 📌 Formula Precision

Precision = (Jumlah Rekomendasi yang Relevan) / (Jumlah Total Rekomendasi)

Sebuah film dianggap *relevan* jika memiliki genre yang sama dengan film acuan.

#### 🧾 Hasil Evaluasi

Sistem diuji dengan memilih film acak sebagai input dan mengeluarkan 10 film teratas berdasarkan skor kemiripan. Hasilnya:

- Semua film yang direkomendasikan memiliki genre yang sama (Action).
- Nilai precision = **1.0**

➡️ Ini menunjukkan bahwa sistem mampu memberikan rekomendasi yang konsisten dan relevan secara konten terhadap film yang menjadi acuan.

---

### 👥 Collaborative Filtering Evaluation

Untuk pendekatan Collaborative Filtering berbasis neural network (Neural Collaborative Filtering), digunakan metrik **Mean Absolute Error (MAE)** karena sistem berfungsi memprediksi rating dari pengguna terhadap film.

#### 📌 Formula MAE

MAE = (1/n) × Σ |rating_aktual - rating_prediksi|

Dimana:
- *rating_aktual*: rating asli dari pengguna.
- *rating_prediksi*: rating yang dihasilkan oleh model.
- *n*: jumlah data pengujian.

#### 🧾 Hasil Evaluasi

- Model dilatih menggunakan teknik embedding user dan item, diikuti oleh lapisan dense dengan regularisasi L2.
- Kurva **training MAE** dan **validation MAE** menunjukkan tren penurunan yang stabil selama pelatihan.
- Hasil akhir menunjukkan nilai **Validation MAE = 0.6461**, yang merupakan indikasi bahwa prediksi rating cukup dekat dengan nilai aktual dan kesalahan model relatif rendah.

➡️ Sistem dapat memprediksi preferensi pengguna terhadap film secara akurat berdasarkan histori rating.

---

### 📌 Evaluasi Terhadap Business Understanding

Mari kita hubungkan hasil evaluasi dengan komponen *Business Understanding*:

| Problem Statement | Apakah Terjawab? | Penjelasan |
|-------------------|------------------|------------|
| 1. Pengguna kesulitan menemukan film yang sesuai | ✅ Ya | Content-Based Filtering memberikan rekomendasi berdasarkan genre dan tag, Collaborative Filtering menggunakan preferensi historis pengguna. |
| 2. Rekomendasi non-personal mengurangi minat | ✅ Ya | Model Collaborative Filtering menghasilkan rekomendasi yang disesuaikan dengan interaksi pengguna tertentu. |
| 3. Sistem sederhana gagal menangkap pola kompleks | ✅ Ya | Neural Collaborative Filtering mampu menangkap pola non-linear melalui arsitektur deep learning. |

| Goals | Status | Penjelasan |
|-------|--------|------------|
| 1. Sistem sesuai minat pengguna | ✅ Tercapai | Sistem menghasilkan rekomendasi relevan baik dari sisi konten maupun histori pengguna. |
| 2. Relevansi & personalisasi meningkat | ✅ Tercapai | Penggunaan dua pendekatan memberikan fleksibilitas dan akurasi lebih tinggi. |
| 3. Implementasi pendekatan modern | ✅ Tercapai | Deep learning digunakan untuk menggantikan metode tradisional collaborative filtering. |

| Solution Statement | Dampak | Penjelasan |
|--------------------|--------|------------|
| Content-Based Filtering | Positif | Mampu memberikan rekomendasi berdasarkan kemiripan konten secara tepat (precision = 1.0). |
| Neural Collaborative Filtering | Positif | Memodelkan preferensi pengguna dengan MAE rendah dan menunjukkan pembelajaran stabil. |

---

### 🧠 Kesimpulan Evaluasi

Kedua pendekatan rekomendasi menunjukkan performa yang baik dan saling melengkapi:

- **Content-Based Filtering** efektif dalam konteks cold-start dan akurasi genre/tag.
- **Collaborative Filtering** lebih personal dan menangkap preferensi pengguna secara eksplisit.

Secara keseluruhan, sistem rekomendasi yang dibangun telah **menjawab seluruh pernyataan masalah, mencapai semua tujuan bisnis, dan memberikan dampak positif terhadap solusi yang dirancang**. Pendekatan hybrid yang menggabungkan kedua metode ini dapat menjadi strategi optimal untuk sistem rekomendasi skala industri.

---


**---Ini adalah bagian akhir laporan---**

