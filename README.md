# Laporan Proyek Machine Learning - Sulistiani

## Project Overview

Peminat industri manga (komik) semakin meningkat, dan telah menjadi budaya yang populer, terkhususnya di kalangan anak muda (Alana & Hartanto, 2024). Berdasarkan data dari Asosiasi Komik Indonesia atau disingkat AKSI pada tahun 2021 yang pernah melakukan penelitian  melalui  media  sosial. Indonesia, diketahui bahwa merupakan negara dengan pembaca komik terbesar ke-4 dunia & ke-2 Asia,  serta  negara  pembaca  manga  atau  komik Jepang  terbesar  ke-3  dunia  &  pertama  Asia.  Dengan jumlah  169  judul  buku  komik  Indonesia  dan  335  judul  komik  digital  rilis  dalam  setahunnya,  serta sekitar, 22,5% pasar buku dikuasai oleh kategori komik dan buku anak (Asosiasi Komik Indonesia, 2021).

Dengan banyaknya jumlah manga (komik) yang telah dirilis, kebanyakan penggemar komik mengalami kesulitan dalam memilih sesuai dengan preferensi. Oleh karena itu, dibutuhkan sebuah sistem rekomendasi yang dapat memberikan saran judul manga (komik) sesuai dengan preferensi pengguna.

Sistem yang akan dibangun menggunakan content-based filtering, yaitu menganalisis kemiripan antar judul manga (komik) berdasarkan fitur kontennya. Diantaranya adalah genre, score, published, dan status. Diharapkan sistem ini dapat memberikan kemudahan bagi pengguna untuk lebih mudah dalam mencari manga (komik) serupa dengan yang sudah pernah mereka baca.


## Business Understanding

### Problem Statements
- Bagaimana pembangunan sistem rekomendasi berdasarkan kemiripan konten seperti genre, skor, tahun terbit, dan status?
- Bagaimana cara sistem mengenali manga yang relevan atau mirip dengan preferensi pengguna sebelumnya?
- Bagaimana efektivitas metode content-based filtering dalam memberikan rekomendasi manga yang sesuai dengan minat pengguna?

### Goals
- Membangun sistem rekomendasi berdasarkan kemiripan konten seperti genre, skor, tahun terbit, dan status
- Membangun sistem rekomendasi yang dapat mengenali manga yang sesuai dengan preferensi pengguna sebelumnya
- Membangun sistem yang efektif untuk memberikan rekomendasi yang sesuai dengan minat pengguna

 ### Solution statements
- Menggunakan metode TF-IDF (Term Frequency-Inverse Document Frequency) untuk mengubah data teks (genre) menjadi representasi numerik dalam bentuk matriks vektor.
- Menggunakan metode Cosine Similarity dalam pembangunan sistem rekomendasi untuk mendapatkan rekomendasi berdasarkan kedekatan konten.
- Menggunakan algoritma K-Nearest Neighbors dalam pembangunan sistem rekomendasi dengan n_neighbors=6 untuk menemukan 6 manga/anime terdekat berdasarkan fitur TF-IDF dan consine.


## Data Understanding
Dataset yang digunakan merupakan kumpulan data simulasi mengenai informasi manga dan anime. Untuk penelitian ini dipilih file manga.csv. Di dalam file tersebut terdapat sejumlah 10.000 data dan 16 fitur di dalamnya. Dataset ini dapat digunakan untuk membangun sebuah sistem rekomendasi. Berikut di bawah ini merupakan link dataset yang digunakan untuk penelitian:
https://www.kaggle.com/datasets/duongtruongbinh/manga-and-anime-dataset

**Variabel-variabel pada dataset manga adalah sebagai berikut**
- Title: Judul manga.
- Score: Skor rata-rata yang diberikan oleh pengguna.
- Vote: Jumlah pengguna yang memberikan penilaian.
- Ranked: Peringkat manga berdasarkan skor.
- Popularity: Peringkat popularitas manga berdasarkan jumlah anggota yang menambahkan manga ke daftar mereka.
- Members: Jumlah anggota yang menambahkan manga ke daftar mereka.
- Favorites: Jumlah anggota yang menandai manga sebagai favorit.
- Volumes: Total jumlah volume yang diterbitkan.
- Chapters: Jumlah chapter yang telah diterbitkan.
- Status: Status penerbitan manga, seperti Finished, Publishing, dll.
- Published: Tanggal atau rentang waktu publikasi manga.
- Genres: Daftar genre yang terkait dengan manga, seperti Action, Romance, dll.
- Themes: Tema atau konsep cerita yang lebih spesifik
- Demographics: Segmentasi demografis target pembaca (misalnya Shounen, Seinen, Josei, dll).
- Serialization: Majalah atau platform tempat manga diserialisasikan.
- Authors: Nama penulis manga.

**Kondisi Data:**
![image](https://github.com/user-attachments/assets/727716b9-757c-4b3c-a97b-163a45c15623)

Terdapat 1789 missing values pada kolom serialization, dan 15 missing values pada kolom author.

![image](https://github.com/user-attachments/assets/3adbc64e-02f7-4a44-b6d3-f2944c5f10f3)


Tidak terdapat duplikat pada dataset yang digunakan

![image](https://github.com/user-attachments/assets/1e68f06d-2dfb-4833-b639-08101571cbc9)


### **Exploratory Data Analysis:**
**Score (Rating)**

![image](https://github.com/user-attachments/assets/5343f714-eb7a-4e7f-b12a-d2720e7d3995)


Manga dengan rating tertinggi berasal dari berbagai macam genre, yang menunjukkan variasi dari selera pembaca. Manga dengan judul  Naruto Shinden Series mewakili genre aksi dan petualangan, sementara Piano no Mori dan Shousetsu Kimi no Na wa. masuk dalam genre drama dan slice of life. Keberadaan genre psychological (NHK ni Youkoso!) dan sci-fi (Boogiepop Series) juga menunjukkan bahwa rating tinggi tidak terbatas pada satu tipe cerita saja, melainkan mencerminkan keberagaman tema dan gaya naratif yang dapat diapresiasi oleh pembaca.

**Published**

![image](https://github.com/user-attachments/assets/2254404c-eb59-44e6-bb9e-8be545ea82b3)


Pada rentang tahun 1950-1990 an jumlah manga yang diterbitkan cenderung sangat sedikit, menunjukkan bahwa pada saat itu industri manga belum begitu populer. Namun, pada rentang tahun 1990-2010 terdapat peningkatan yang signifikan terhadap industri manga. Rentang tahun tersebut merupakan masa keemasan industri manga didorong oleh keberhasilan dari manga seperti Naruto, Bleach, One Piece, dan Death Note.

Akan tetapi, pada tahun 2010 keatas terjadi penurunan terhadap jumlah manga yang diterbitkan. Kemudian pada tahun 2020 ke atas terjadi fluktuasi terhadap jumlah manga yang terbit.

**Status**

![image](https://github.com/user-attachments/assets/49abd349-a9b9-45e0-8e89-be756c6e1661)


Sebanyak 78% manga yang terdapat dalam dataset berstatus Finished, menunjukkan bahwa mayoritas manga telah menyelesaikan ceritanya secara penuh. Sementara itu, 20% manga masih berstatus Publishing, menandakan bahwa masih banyak judul yang aktif dan terus diperbarui. Hanya sekitar 1% manga yang berstatus On Hiatus, yaitu sedang dalam masa jeda dan belum diketahui kapan akan dilanjutkan. Adapun manga yang berstatus Discontinued sangat sedikit, yaitu kurang dari 1%, yang berarti manga tersebut telah dihentikan penerbitannya secara permanen. Hal ini menunjukkan bahwa sebagian besar manga dalam dataset memiliki kelanjutan cerita yang stabil dan minim risiko dihentikan.

**Genre**

![image](https://github.com/user-attachments/assets/45185653-a5ea-480f-adda-693ac1a149b6)


Genre Comedy menduduki peringkat pertama dengan jumlah manga terbanyak, disusul oleh genre Action dan Romance, yang juga menunjukkan angka tinggi dalam distribusinya. Genre seperti Supernatural dan Drama menempati posisi menengah, menunjukkan popularitas yang cukup signifikan.


## Data Preparation
### **Tahapan**
**Data Cleaning**
Langkah awal dalam preprocessing data adalah menghapus kolom-kolom yang tidak diperlukan atau kurang relevan untuk analisis, seperti kolom Themes, Demographics, Serialization, Members, dan Favorite. Selanjutnya, dilakukan pembersihan data kosong khususnya pada kolom Genres dengan menghapus baris yang memiliki nilai kosong atau hanya berisi tanda kurung kosong '[]', agar data yang digunakan benar-benar valid dan bermakna.
Untuk mengatasi masalah data numerik yang mengandung outliers, metode Interquartile Range (IQR) digunakan. Pertama, nilai kuartil pertama (Q1) dan kuartil ketiga (Q3) dihitung untuk masing-masing fitur numerik, kemudian IQR dihitung sebagai selisih Q3 dan Q1. Data yang memiliki nilai di luar rentang normal 
[Q1−1.5×IQR,Q3+1.5×IQR] dianggap outliers dan dikeluarkan dari dataset. Data yang sudah difilter tersebut kemudian digabungkan kembali dengan kolom-kolom kategorikal agar dataset yang digunakan sudah bersih dari outliers serta tetap mempertahankan informasi penting lainnya.
**Data Transformation:**
1. Encoding: Kolom Genres diubah menjadi format string agar dapat diolah lebih lanjut. Selanjutnya, data dalam kolom tersebut dipisahkan berdasarkan koma untuk membentuk daftar genre, lalu dikonversi ke dalam format one-hot encoding menggunakan metode get_dummies(). Hasil dari encoding ini berupa representasi biner dari masing-masing genre yang memudahkan algoritma machine learning dalam membaca fitur kategori tersebut.
2. Feature engineering: Menghapus kolom non-fitur seperti Title dan Genres, sehingga hanya menyisakan variabel yang relevan untuk pelatihan model. Proses ini bertujuan untuk menjaga fokus model pada informasi yang benar-benar berpengaruh terhadap output.
3. Handling missing value: Dilakukan pembersihan data dengan mengganti nilai seperti 'Unknown', '-', dan 'Not available' menjadi NaN. Kemudian, setiap kolom dicek apakah bertipe objek, dan jika iya, diubah ke format numerik menggunakan pd.to_numeric agar dapat diolah lebih lanjut. Setelah itu, pada proses feature selection, kolom-kolom numerik yang memiliki nilai hilang diisi menggunakan nilai median dari kolom tersebut. Jika median tidak tersedia (misalnya karena seluruh data kosong), nilai default yang digunakan adalah 0. Proses ini memastikan bahwa tidak ada nilai kosong yang tersisa dalam data.
4. Feature Selection: Sebagai langkah akhir dari transformasi, hasil one-hot encoding genre digabungkan kembali dengan data fitur utama menggunakan pd.concat(), sehingga menghasilkan dataset akhir (X_with_genres) yang siap digunakan untuk pelatihan model machine learning. Proses transformasi ini penting untuk memastikan bahwa seluruh data berada dalam format numerik yang bersih, terstruktur, dan bebas dari nilai yang hilang.

## Modeling
1. **Content Based Filtering**
Dalam proses Content-Based Filtering (CBF) untuk rekomendasi manga atau anime, data teks berupa genre tiap judul diubah menjadi representasi numerik menggunakan metode TF-IDF (Term Frequency-Inverse Document Frequency). TF-IDF memberikan bobot pada setiap kata (genre) yang merefleksikan seberapa penting kata tersebut dalam sebuah dokumen (manga) relatif terhadap keseluruhan koleksi. Dengan cara ini, genre yang umum dan kurang informatif akan diberi bobot lebih rendah, sedangkan genre yang unik dan spesifik akan memiliki bobot lebih tinggi. Setelah data genre diubah menjadi matriks TF-IDF, kemiripan antar manga dihitung menggunakan cosine similarity, yang mengukur sudut kosinus antara dua vektor fitur. Nilai cosine similarity yang tinggi menunjukkan bahwa dua manga memiliki kemiripan genre yang kuat, sehingga dapat direkomendasikan satu sama lain. Matriks similarity ini kemudian digunakan untuk memberikan rekomendasi berdasarkan manga yang dipilih pengguna, dengan mengambil manga-manga yang memiliki nilai kemiripan tertinggi. Pendekatan ini memungkinkan sistem rekomendasi memberikan hasil yang relevan dengan preferensi pengguna berdasarkan kesamaan konten genre.

Kelebihan
- Personalisasi yang Baik: Rekomendasi didasarkan langsung pada karakteristik konten yang sudah disukai pengguna, sehingga hasilnya relevan dengan preferensi individu.
- Tidak Butuh Data Rating dari Banyak Pengguna: Karena hanya menggunakan data atribut konten (genre), metode ini tidak bergantung pada data interaksi pengguna yang lengkap seperti rating atau klik.
- Mudah Diinterpretasikan: Sistem dapat menjelaskan rekomendasi berdasarkan kesamaan atribut (misal genre yang sama), sehingga lebih transparan dan mudah dipahami.
- Efisien untuk Data Teks: TF-IDF efektif mengubah data teks menjadi fitur numerik dengan bobot yang mencerminkan pentingnya kata, membantu memfilter informasi yang kurang relevan.

Kekurangan
- Keterbatasan dalam Rekomendasi Diversifikasi: Sistem cenderung merekomendasikan item yang sangat mirip dengan yang sudah diketahui pengguna, sehingga kurang mampu memberikan rekomendasi yang berbeda atau mengeksplorasi preferensi baru.
- Masalah Cold-Start untuk Item Baru: Jika ada item baru tanpa metadata atau atribut konten lengkap, sistem sulit memberikan rekomendasi yang akurat untuk item tersebut.
- Ketergantungan pada Kualitas Fitur: Hasil sangat bergantung pada kualitas dan kelengkapan fitur konten. Misalnya, jika genre kurang representatif atau kurang deskriptif, rekomendasi bisa jadi kurang relevan.
- Tidak Memperhitungkan Preferensi Kolektif: Karena fokus pada konten dan bukan pola interaksi pengguna secara luas, sistem tidak memanfaatkan kekuatan data kolaboratif yang bisa menangkap tren atau pola popularitas.


![alt text](image-9.png)


2. **K-Nearest Neighbor (KNN)**
Pendekatan K-Nearest Neighbors (KNN) digunakan untuk merekomendasikan manga yang serupa berdasarkan jarak atau kesamaan dalam ruang fitur numerik yang telah dipersiapkan sebelumnya (misalnya, fitur metadata atau embedding). Ketika pengguna mencari rekomendasi untuk judul tertentu, seperti "One Piece", sistem akan mencari indeks manga tersebut dalam dataset dan mengambil vektor fitur yang merepresentasikan manga tersebut. Selanjutnya, algoritma KNN menghitung jarak antara vektor fitur manga tersebut dengan semua manga lain dalam dataset, kemudian memilih sejumlah manga terdekat (neighbors) berdasarkan jarak terkecil. Manga-manga yang berada paling dekat secara fitur ini dianggap paling mirip dan direkomendasikan kepada pengguna. Jarak yang digunakan bisa berupa Euclidean, cosine, atau metrik lain sesuai kebutuhan, dan hasilnya berupa daftar rekomendasi yang diurutkan dari yang paling mirip hingga kurang mirip, lengkap dengan nilai jarak sebagai ukuran kemiripan. Pendekatan ini memungkinkan sistem menangkap kesamaan yang lebih kompleks berdasarkan fitur multi-dimensi dan tidak hanya terbatas pada kesamaan konten sederhana.

Kelebihan KNN:
- Menangkap kesamaan kompleks antar item berdasarkan berbagai fitur numerik.
- Mudah diimplementasikan dan tidak memerlukan pelatihan model yang rumit.
- Non-parametrik, fleksibel untuk berbagai jenis data dan pola.
- Memberikan rekomendasi yang beragam, tidak terbatas pada satu atribut saja.

Kekurangan KNN:
- Kurang efisien pada dataset besar, karena harus hitung jarak ke semua data.
- Kualitas rekomendasi tergantung pada fitur, jika fitur kurang baik hasil juga kurang akurat.
- Perlu pemilihan parameter yang tepat (jumlah tetangga k dan metrik jarak).
- Tidak adaptif terhadap perubahan preferensi pengguna, karena hanya berdasarkan kemiripan antar item.

![alt text](image-10.png)


## Evaluation
Dalam proyek sistem rekomendasi manga ini, evaluasi kinerja dilakukan menggunakan dua metrik utama yaitu Precision@5 dan Recall@5. Kedua metrik ini sangat relevan dalam konteks rekomendasi karena mengukur seberapa baik sistem dalam memberikan daftar rekomendasi yang relevan dalam jumlah terbatas (top 5).

Precision@k (di sini k=5) dihitung dengan rumus:

![alt text](image-11.png)

Recall@k (k=5) dihitung dengan rumus:

![alt text](image-12.png)

Hasil evaluasi pada proyek ini menunjukkan nilai rata-rata Precision@5 sebesar 0.47 dan Recall@5 sebesar 1.00 untuk kedua metode Content-Based Filtering (CBF) dan K-Nearest Neighbors (KNN).

| Metode                        | Precision@5 | Recall@5 |
|-------------------------------|-------------|----------|
| Content-Based Filtering (CBF) | 0.47        | 1.00     |
| K-Nearest Neighbors (KNN)     | 0.47        | 1.00     |

Artinya, sekitar 47% dari 5 rekomendasi yang diberikan benar-benar relevan dengan preferensi pengguna, sementara seluruh item relevan pengguna (100%) berhasil masuk ke dalam rekomendasi tersebut. Dengan recall sempurna, sistem dapat memenuhi kebutuhan pengguna secara lengkap, walaupun masih ada ruang untuk meningkatkan precision agar rekomendasi menjadi lebih akurat dan minim item yang tidak relevan.

Secara keseluruhan, metrik ini menunjukkan bahwa kedua metode memberikan performa yang cukup baik dalam menyediakan rekomendasi yang relevan dan komprehensif pada dataset yang digunakan.


## **Referensi**
Alana, R., & Hartanto, A. (2024). Implementation of Content Based Filtering Algorithm in Comic Recommendation System. Sistemasi: Jurnal Sistem Informasi, 13(4), 1344-1355.
Asosiasi Komik Indonesia, “Komik Sebagai Lokomotif Industri Haki,” 2021, [Online],
Available: https://facebook.com/asosiasikomik/posts/104480355050879
