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
Proyek ini menggunakan Book-Crossing Dataset yang tersedia secara publik melalui platform Kaggle. Dataset ini berisi informasi mengenai buku, pengguna, dan penilaian (rating) yang diberikan oleh pengguna terhadap buku tersebut.

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
