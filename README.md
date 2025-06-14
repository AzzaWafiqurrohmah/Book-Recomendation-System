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

Tahapan data preparation dilakukan untuk memastikan bahwa data yang digunakan dalam proses pemodelan sudah bersih, relevan, dan dalam format yang sesuai.  
Seluruh proses disesuaikan dengan kebutuhan dua pendekatan sistem rekomendasi yang digunakan, yaitu **Content-Based Filtering** dan **Collaborative Filtering**.

### 1. Data Cleaning

- **Menghapus rating dengan nilai nol**  
  Rating bernilai 0 tidak mencerminkan preferensi eksplisit dari pengguna dan lebih merepresentasikan implicit feedback.  
  Untuk menjaga akurasi dan distribusi data, nilai-nilai ini dihapus agar tidak mempengaruhi performa model.

- **Memfilter buku berdasarkan data rating**  
  Diambil 10.000 buku dengan jumlah rating terbanyak dari dataset yang telah dibersihkan.  
  Langkah ini bertujuan mengurangi *sparsity* dan mengoptimalkan proses komputasi.

- **Memfilter data user**  
  Dataset pengguna disesuaikan hanya mencakup user yang benar-benar memberikan rating.  
  Hal ini menghindari keberadaan entitas tidak relevan yang dapat mengganggu performa model.

- **Konversi tipe data**  
  Kolom ISBN dikonversi ke tipe string untuk menjaga konsistensi format.  
  Kolom Book-Rating dikonversi ke tipe float32 agar efisien dalam perhitungan numerik.

### 2. Data Preprocessing

- **Menggabungkan dataset ratings dengan books**  
  Dataset rating yang telah difilter digabungkan dengan data buku berdasarkan kolom ISBN.  
  Ini diperlukan untuk menyediakan informasi konten tambahan bagi pendekatan Content-Based Filtering.

- **Pemeriksaan data null dan duplikat**  
  Setelah penggabungan data, dilakukan pengecekan terhadap nilai kosong dan duplikat untuk memastikan konsistensi dan integritas data.

- **Menghapus kolom yang tidak dibutuhkan**  
  Kolom seperti Image-URL-S, Image-URL-M, dan Image-URL-L dihapus karena tidak relevan untuk proses pemodelan.

- **Membuat dataframe unik berisi informasi buku**  
  Disusun dataframe dengan kombinasi unik ISBN, judul, penulis, dan penerbit untuk memastikan keunikan dan validitas entitas buku.

- **Menggabungkan kolom penulis dan penerbit**  
  Kolom Book-Author dan Publisher digabung menjadi satu kolom teks sebagai representasi konten buku.

- **Ekstraksi fitur dengan TF-IDF Vectorization**  
  Kolom gabungan penulis dan penerbit diekstrak menggunakan teknik TF-IDF untuk menghasilkan representasi numerik berbasis teks, yang akan digunakan dalam Content-Based Filtering.

- **Encoding ID pengguna dan buku**  
  ID user dan ID buku dikodekan ke bentuk numerik untuk keperluan embedding dan input ke model Collaborative Filtering.

- **Normalisasi nilai rating**  
  Nilai Book-Rating dinormalisasi ke rentang antara 0 dan 1. Normalisasi ini penting untuk membantu proses pelatihan model neural network pada pendekatan Collaborative Filtering.

- **Pengacakan (shuffling) data**  
  Dataset diacak menggunakan `df.sample(frac=1)` untuk menghindari bias urutan sebelum proses training.

- **Split data menjadi training dan validation**  
  Dataset akhir dibagi menjadi dua bagian: data latih dan data validasi, untuk keperluan evaluasi performa model.


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
Sebagai hasil akhir, sistem menghasilkan Top-5 rekomendasi buku untuk setiap pengguna. Contoh dari masing masing model seperti dibawah ini: 

#### 1. Content-Based Filtering
Model ini merekomendasikan buku berdasarkan kemiripan fitur konten, seperti penulis dan penerbit. Sistem akan mencari buku yang memiliki kemiripan dengan buku yang pernah disukai oleh pengguna.

Contoh 5 rekomendasi teratas untuk buku "Shades Of Twilight" dengan penulis Linda Howard dan penerbit Pocket adalah:
- Son of the Morning, Linda Howard, Pocket
- Strangers in the Night, Linda Howard, Pocket
- Open Season, Linda Howard, Pocket
- Everlasting Love, Linda Howard, Pocket
- Dying to Please, Linda Howard, Ballantine Books

#### 2. Collaborative Filtering
Model ini memanfaatkan perilaku pengguna lain yang serupa untuk memberikan rekomendasi. Sistem akan merekomendasikan buku berdasarkan preferensi pengguna lain yang memiliki pola kesukaan serupa.

Contoh Output untuk User ID 34502
- Buku dengan rating tinggi dari user:
   - Exclusive – Sandra Brown, Warner Books
   - An Isolated Incident – Susan R. Sloan, Warner Books

- Top-5 Rekomendasi:
   - Mere Christianity – C. S. Lewis, Macmillan Pub. Co
   - The Hobbit – J. R. R. Tolkien, Ballantine Books
   - The Tomb and Other Tales – H. P. Lovecraft, Del Rey Books
   - A Swiftly Tilting Planet – Madeleine L'Engle, Farrar, Straus and Giroux
   - Daughter of the Blood – Anne Bishop, Roc


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
Berbeda dengan collaborative filtering yang menggunakan metrik numerik seperti MAE, evaluasi pada pendekatan content-based filtering awalnya dilakukan secara kualitatif berdasarkan relevansi hasil rekomendasi. Model content-based ini merekomendasikan buku kepada pengguna berdasarkan kemiripan atribut konten buku, seperti judul, nama penulis, dan penerbit. Evaluasi dilakukan dengan mengamati seberapa relevan dan bervariasi hasil rekomendasi terhadap item tertentu.

Meskipun pendekatan ini tidak mengalami masalah sparsity seperti collaborative filtering, kelemahan utamanya terletak pada kecenderungan sistem merekomendasikan buku yang terlalu mirip (kurang bervariasi), yang dikenal sebagai serendipity problem. Secara keseluruhan, model content-based ini memberikan hasil yang relevan dan cocok untuk pengguna baru (cold start), namun memiliki keterbatasan dalam mengeksplorasi item di luar preferensi awal pengguna.

Untuk melengkapi evaluasi, dilakukan juga pengukuran kuantitatif menggunakan metrik:
- Precision@5 (seberapa banyak dari top-5 rekomendasi yang benar-benar relevan)
- Recall@5 (seberapa banyak dari total buku relevan yang berhasil direkomendasikan)

Evaluasi dilakukan dengan membagi sebagian data sebagai test set, dan mengukur relevansi rekomendasi terhadap data ground truth pengguna (buku-buku yang sebelumnya diberi rating tinggi).

Hasil evaluasi kuantitatif:
- Precision@5: 0.0118
- Recall@5: 0.0323

Nilai ini menunjukkan bahwa model content-based filtering masih memiliki keterbatasan dalam menjangkau preferensi pengguna secara akurat, kemungkinan besar karena keterbatasan fitur konten yang digunakan (hanya penulis dan penerbit). Meski demikian, model ini tetap bermanfaat sebagai baseline dan dapat diperkuat dengan penambahan fitur seperti genre, deskripsi, atau sinopsis untuk meningkatkan akurasi rekomendasi.

