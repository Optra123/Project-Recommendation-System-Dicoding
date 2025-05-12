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
![Gambar tag paling populer](https://github.com/undagie/Dicoding-Recomendation-System/blob/main/img/tag.png?raw=true)

- **Genre populer** di dataset ini termasuk Drama, Comedy, dan Action.
- **Pola user-film** menunjukkan bahwa sebagian besar pengguna hanya menilai sebagian kecil dari total film, menunjukkan sifat sparsity yang umum dalam sistem rekomendasi.

Visualisasi dan pembersihan data akan dilakukan untuk memastikan kualitas dan konsistensi data sebelum masuk ke tahap pemodelan.


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
