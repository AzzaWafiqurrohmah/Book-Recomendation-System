# Laporan Proyek Machine Learning - Azza Wafiqurrohmah

## Project Overview

Dalam era digital yang terus berkembang, akses terhadap informasi menjadi semakin luas dan cepat. Hal ini juga berlaku dalam dunia literasi, di mana pengguna dihadapkan pada ribuan bahkan jutaan pilihan buku yang tersedia secara online. Banyaknya pilihan ini sering kali menimbulkan fenomena information overload, yaitu kondisi di mana pengguna kesulitan menyaring dan memilih buku yang sesuai dengan minat dan kebutuhannya.

Situasi ini menekankan pentingnya peran sistem rekomendasi sebagai alat bantu dalam proses pengambilan keputusan. Dengan kemampuan untuk menyajikan informasi yang relevan secara otomatis, sistem rekomendasi dapat meningkatkan pengalaman pengguna dan efisiensi dalam pencarian konten. Dalam konteks ini, pengembangan sistem rekomendasi buku menjadi solusi penting yang dapat membantu pengguna menemukan buku yang sesuai dengan preferensi mereka dengan lebih cepat dan akurat.

Seiring dengan meningkatnya kebutuhan akan sistem rekomendasi yang cerdas dan adaptif, berbagai pendekatan telah dikembangkan, seperti Content-Based Filtering yang mempertimbangkan karakteristik item, serta Collaborative Filtering yang memanfaatkan pola interaksi antar pengguna. Pemanfaatan kedua pendekatan ini mencerminkan perkembangan teknologi rekomendasi yang terus diarahkan untuk menangani tantangan seperti kelangkaan data (data sparsity) dan masalah pengguna baru (cold start), yang kerap muncul dalam implementasi di dunia nyata.

## Business Understanding

### Problem Statement
Di tengah maraknya platform digital yang menyediakan jutaan judul buku, pengguna sering kali kesulitan dalam menemukan buku yang sesuai dengan minat dan preferensinya. Ketidaksesuaian antara banyaknya pilihan dengan keterbatasan waktu dan perhatian pengguna menyebabkan munculnya tantangan dalam memberikan pengalaman membaca yang personal dan efisien. Sistem rekomendasi yang tidak akurat dapat menyebabkan penurunan minat pengguna serta mengurangi efektivitas platform dalam mempertahankan keterlibatan mereka.


### Goals
Tujuan utama dari proyek ini adalah untuk membangun sistem rekomendasi buku yang mampu memberikan saran bacaan yang relevan dan personal kepada pengguna. Sistem ini diharapkan dapat:
- Membantu pengguna menemukan buku yang sesuai dengan preferensi mereka.
- Meningkatkan keterlibatan pengguna dengan platform.
- Mengurangi efek information overload dengan memberikan pilihan yang terkurasi.

### Solution Approach
Untuk mencapai tujuan tersebut, dua pendekatan utama digunakan dalam pengembangan sistem rekomendasi ini:
- Content-Based Filtering
   Pendekatan ini merekomendasikan buku berdasarkan kemiripan kontennya. Sistem akan menganalisis fitur-fitur dari buku (seperti judul dan kategori) yang telah diberi rating tinggi oleh pengguna, lalu mencari buku lain yang memiliki karakteristik serupa. Metode ini efektif dalam memberikan rekomendasi yang konsisten dengan preferensi pengguna individu.
- User-Based Collaborative Filtering
   Dalam pendekatan ini, sistem memanfaatkan pola perilaku pengguna lain untuk memberikan rekomendasi. Sistem akan mencari pengguna lain yang memiliki preferensi serupa, lalu merekomendasikan buku yang disukai oleh pengguna-pengguna tersebut. Metode ini berpotensi menemukan buku baru yang belum pernah dijelajahi oleh pengguna tetapi relevan karena pola kesukaan yang mirip.

Kombinasi dari dua pendekatan ini diharapkan dapat meningkatkan akurasi dan relevansi sistem rekomendasi secara keseluruhan.


## Data Understanding
### Dataset Overview
Pada proyek ini, dataset yang digunakan adalah Book-Crossing Dataset yang tersedia secara publik melalui platform Kaggle melalui tautan berikut: https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset. Dataset ini berisi informasi mengenai buku, pengguna, dan penilaian (rating) yang diberikan oleh pengguna terhadap buku tersebut.

Dataset terdiri dari tiga file utama:
1. Books.csv – berisi informasi detail tentang buku.
2. Users.csv – berisi informasi dasar pengguna.
3. Ratings.csv – berisi data interaksi berupa rating yang diberikan oleh pengguna terhadap buku.

### Jumlah dan Kondisi Data
Setelah dilakukan penggabungan dan pembersihan data awal, diperoleh ringkasan sebagai berikut:

- Jumlah data rating awal: 1.149.780 entri
- Jumlah rating bernilai 0 (tidak memberi penilaian): 716.109 entri
- Jumlah rating non-0 yang digunakan: 175.542 entri
- Jumlah buku unik setelah disaring: 9.548 buku
- Jumlah pengguna aktif: 65.000+ user
- Total data rating yang digunakan setelah filter: 175.542 entri

Rating yang bernilai 0 dianggap sebagai interaksi non-informatif dan tidak digunakan dalam proses pelatihan model rekomendasi karena tidak merepresentasikan preferensi pengguna.

### Penjelasan Variabel
Berikut penjelasan variabel dari masing-masing file:

### 📚 Books.csv

| Kolom               | Deskripsi                                           |
|---------------------|-----------------------------------------------------|
| ISBN                | Nomor identifikasi unik untuk setiap buku           |
| Book-Title          | Judul buku                                          |
| Book-Author         | Nama penulis buku                                   |
| Year-Of-Publication | Tahun terbit buku                                   |
| Publisher           | Nama penerbit buku                                  |
| Image-URL-S         | Link gambar sampul buku (ukuran kecil)              |
| Image-URL-M         | Link gambar sampul buku (ukuran sedang)             |
| Image-URL-L         | Link gambar sampul buku (ukuran besar)              |


### 👤 Users.csv

| Kolom    | Deskripsi                                                                       |
|----------|----------------------------------------------------------------------------------|
| User-ID  | ID unik pengguna                                                                |
| Location | Lokasi pengguna (biasanya dalam format “kota, negara bagian, negara”)           |
| Age      | Usia pengguna (terdapat missing value dan nilai outlier)                        |


### ⭐ Ratings.csv

| Kolom       | Deskripsi                                                                 |
|-------------|---------------------------------------------------------------------------|
| User-ID     | ID pengguna yang memberikan rating                                        |
| ISBN        | ISBN buku yang dinilai                                                    |
| Book-Rating | Nilai rating yang diberikan pengguna terhadap buku (skala 0–10)           |

## Exploratory Data Analysis (EDA)
Beberapa tahapan EDA dilakukan untuk memahami pola dalam data. Berikut beberapa insight yang diperoleh:

### 1. Distribusi Rating
  ![image](https://github.com/user-attachments/assets/7bd0d65c-ee97-417a-9445-2a218ece9b37)

### 2. Top Buku Paling Banyak Dinilai
![image](https://github.com/user-attachments/assets/06497897-77f3-4c57-8c90-82224abcc4f0)

### 3. Pengguna Paling Aktif
![image](https://github.com/user-attachments/assets/efd4cdf6-87c0-455b-addc-75fb979ac4af)


## Data Preparation
Tahapan data preparation dilakukan untuk memastikan bahwa data yang digunakan dalam proses pemodelan sudah bersih, relevan, dan dalam format yang sesuai. Seluruh teknik yang diterapkan dilakukan secara berurutan dan disesuaikan dengan kebutuhan dua pendekatan sistem rekomendasi: Content-Based Filtering dan Collaborative Filtering.

### 1. Data Cleaning
- Menghapus rating dengan nilai nol
Data dengan nilai rating 0 tidak mencerminkan preferensi pengguna dan hanya berfungsi sebagai implicit feedback, sehingga dihapus agar tidak mengganggu distribusi data dan performa model.

- Memfilter buku berdasarkan data rating
Dipilih 10.000 buku dengan jumlah rating terbanyak dari dataset rating yang telah dibersihkan. Hal ini dilakukan untuk mengurangi sparsity dan mengatasi keterbatasan sumber daya komputasi.

- Memfilter data user
Dataset user disesuaikan agar hanya mencakup pengguna yang benar-benar memberikan rating. Langkah ini bertujuan untuk menghilangkan entitas yang tidak relevan.


### 2. Data Preprocessing
- Menggabungkan dataset ratings dengan books
Dataset rating difilter digabung dengan data buku berdasarkan kolom ISBN untuk memperoleh informasi tambahan yang dibutuhkan oleh model Content-Based Filtering.

- Pemeriksaan data null dan duplikat
Setelah penggabungan, dilakukan pengecekan terhadap nilai kosong dan data duplikat untuk menjaga kualitas dan konsistensi data.

- Menghapus kolom yang tidak dibutuhkan
Tiga kolom berupa URL gambar (Image-URL-S, Image-URL-M, Image-URL-L) dihapus karena tidak diperlukan dalam proses pemodelan.

- Membuat dataframe unik berisi informasi buku
Disusun dataframe yang hanya berisi kombinasi unik dari ISBN, judul, penulis, dan penerbit untuk memastikan data yang digunakan benar-benar valid dan representatif.

- Menggabungkan kolom penulis dan penerbit
Kolom Book-Author dan Publisher digabungkan sebagai representasi konten untuk proses ekstraksi fitur dalam Content-Based Filtering.

- Encoding ID pengguna dan buku
ID pengguna dan ID buku diubah ke dalam bentuk representasi numerik menggunakan encoding. Langkah ini diperlukan agar data dapat digunakan dalam proses embedding pada model Collaborative Filtering.



## Modeling
Pada proyek ini, dikembangkan dua pendekatan sistem rekomendasi yang berbeda:

### 1. Content-Based Filtering
Pendekatan ini merekomendasikan buku berdasarkan kemiripan konten dengan buku yang telah disukai oleh pengguna. Fitur yang digunakan adalah judul buku, penulis, dan penerbit, yang digabung lalu diproses menggunakan TF-IDF vectorizer. Kemiripan antar buku dihitung menggunakan cosine similarity.

- Kelebihan:
   - Tidak bergantung pada jumlah pengguna atau rating.
   - Mampu memberikan rekomendasi meskipun buku belum pernah diberi rating (mengurangi cold-start pada item).
     
- Kekurangan:
   - Hanya merekomendasikan buku yang mirip dengan apa yang sudah disukai.
   - Tidak mempertimbangkan preferensi komunitas atau perilaku pengguna lain.

### 2. Collaborative Filtering (User–Item Matrix Factorization)
Pendekatan ini memanfaatkan data interaksi pengguna dengan buku berupa rating. Sistem dilatih menggunakan arsitektur embedding neural network (RecommenderNet), yang memetakan pengguna dan buku ke dalam vektor laten, lalu menghitung interaksi antar keduanya.

- Kelebihan:
   - Mampu menangkap pola kompleks dalam preferensi pengguna.
   - Mampu merekomendasikan buku yang tidak serupa secara konten, namun disukai oleh pengguna dengan perilaku serupa.
     
- Kekurangan:
   - Rentan terhadap masalah cold-start (jika pengguna atau item baru tidak punya cukup data).
   - Membutuhkan data interaksi yang cukup banyak dan berkualitas.

### Output Top-N Recommendation
Sebagai hasil akhir, sistem menghasilkan Top-10 rekomendasi buku untuk setiap pengguna. Rekomendasi ini didasarkan pada skor prediksi tertinggi dari model yang telah dilatih dan tidak termasuk buku yang sudah pernah diberi rating sebelumnya oleh pengguna tersebut.

## Evaluation

### 1. Collaborative Filtering

![image](https://github.com/user-attachments/assets/ab3ca541-4857-4e7c-9b51-85e5d67f2a9c)


Evaluasi model dilakukan menggunakan Mean Absolute Error (MAE) yang mengukur rata-rata selisih absolut antara rating prediksi dan rating aktual.
Rumus MAE:
<p align="center">
  MAE = (1/n) * Σ | yᵢ - ŷᵢ | <br>
</p>
Hasil Evaluasi
Berdasarkan grafik pelatihan, model menunjukkan penurunan MAE yang konsisten pada data pelatihan maupun validasi seiring bertambahnya epoch. Nilai MAE pada data validasi cenderung stabil di sekitar 0.18–0.19, menandakan bahwa model memiliki performa generalisasi yang baik dan tidak mengalami overfitting. Hal ini menunjukkan bahwa model mampu memberikan prediksi rating yang cukup akurat terhadap preferensi pengguna.

### 2. Content-Based Filtering
Berbeda dengan collaborative filtering yang menggunakan metrik numerik seperti MAE, evaluasi pada pendekatan content-based filtering dilakukan secara kualitatif berdasarkan relevansi hasil rekomendasi. Model content-based ini merekomendasikan buku kepada pengguna berdasarkan kemiripan atribut konten buku, seperti judul, nama penulis, dan penerbit. Evaluasi dilakukan dengan mengamati seberapa relevan dan bervariasi hasil rekomendasi terhadap item tertentu.

Meskipun pendekatan ini tidak mengalami masalah sparsity seperti collaborative filtering, kelemahan utamanya terletak pada kecenderungan sistem merekomendasikan buku yang terlalu mirip (kurang bervariasi). Hal ini disebut serendipity problem. Secara keseluruhan, model content-based ini memberikan hasil yang relevan dan cocok untuk pengguna baru (cold start), namun memiliki keterbatasan dalam mengeksplorasi item di luar preferensi awal pengguna.

