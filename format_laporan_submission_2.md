# Laporan Proyek Machine Learning - Rayhan Gibrani Uhum 

## Project Overview

Dengan berkembangnya layanan live streamin seprti disney plus , netflix dan lain lain , tentu membuat para penonton menjadi nemiliki banyak pilihan .Terkadang penonton setelah menonton sebuah film ingin menonton film lainnya yang memiliki karakteristik sama .oleh sebab itu , adanya projek ini untuk membantu penonton / pecinta film untuk menikmati series atau film setelah series kesayangan mereka selesai.
  
  Format Referensi: [Judul Referensi](https://scholar.google.com/) 

## Business Understanding

seperti yang teah di bahas pada sub bab sebelumnya , tentunya akan mempermudah user untuk menemukan film atau series yang sesuai dengan yang mereka sukai , selain daripada itu sitem ini dapat menguntungkan kedua belah pihak baik sebagai user ataupun pemilik layanan.

Bagian laporan ini mencakup:

### Problem Statements

-  bagaimana cara  memberikan rekomendasi film yang sesuai dengan user dan menjadi relavan dan sesuai dengan selera dari prilaku user dan rating pengguna.
-  bagaimana hasil evaluasi dari model rekomendasi relevan dan sesuai dengan prilaku dan rating dari pengguna lain. 
### Goals
dalam projek ini tujuan  yang ingin di capai seperti pada poin di bawah.

-  mengetahui cara mengetahui film yang relevan dengan pengguna, serta mengevaluasi model tersebut .

-  memberikan hasil rekomendasi dari  model yang relevan denngan selera dan rating pengguna lain. 

    ### Solution statements
  setelah memaparkkan apa _problem statement_ dan  * *Goals* *, pada projek ini akan memberikan solusi  sebagai beriku:  
  - melakukan eksplorasi data dari data set yang digunakan pada projek ini, dan melakukan pembersihan data serta memilah feature yang akan di gunakan pada model rekomendasi.
  - pada projek ini menggunakan 2 teknik  yaitu _Content-Based filtering_ dan * *colaborative filtering**. kedua metode ini sangat relevan mengingat  dalam merekomedasikan film user cenderung melihat genre serta rating pada film .

## Data Understanding
Pada projek ini kami menggunakan data set dari movie lens yang khusus untuk penggunaan dengan tujuan pembelajaran. yang berisi 100,0000 rating , 3,600 tag dan 9000 film .Dataset ini dapat di dwnload melalui link berikut :

https://grouplens.org/datasets/movielens/

dalam projek ini memiliki beberapa file diantaranya film , ratinig , link. dan tag. setiap file mewakili sesuatu seperti :
- **file film* * yang berisi list film  dan genre yang dimiliiki oleh film tersebut
- * *file rating** yang berisi jumlah user yang memberikan rating dan nilai rating yang mereka berika sesuai dengan feature moviId
- * *file tag** yang berisi tag dan timestamp dimana user berhenti atau mengklik
- * *file link"" yang berisi link menuju film

setelah membahas file yang ada dalam * *zip** grouplens/movielens tentunya selanjutnya adalah penjelasan dari setiap featur yang ada dalam projek ini :

- movies.csv
  
  | faeature | penjelasan |
  | --- | --- |
  |movieId | ID (nomor identitas) bagi setiap film |
  |title | memuat judul |
  |genre | memuat genre pada film |

- rating.csv.

  | feature | penjelasan |
  | --- | ---|
  |userId | memuat nomor Id setiap * *user** dalam data |
  |movieId | memuaat ID dalam setiap film |
  | rating | memuar rating dari seriap user dengan skala dari 1 sampai dengan 5. |
  | time stamp | memuar timestamp |
  
- tags .csv

  |feature | penjelasan |
  | --- | --- |
  |userId | memuat nomor ID dari * *user** / pengguna |
  | movieId | memuat nomor ID dari setiap  film |
  | tag | memuar  tah dari film |
  |time stamp | memuat **timestamp* * dari film |

- links.csv

  |feature | penjelasan |
  | --- | --- |
  | movieId | berisi tentang ID dari film |
  | imdbId | memuat nomor ID fim yang merujuk pada website IMDb |
  | tmbId | memuat nomor ID film yang merujuk pada website TMDB |


**Rubrik/Kriteria Tambahan (Opsional)**:
- Melakukan beberapa tahapan yang diperlukan untuk memahami data, contohnya teknik visualisasi data beserta insight atau exploratory data analysis.

## Data Preparation
dalam menyelasaikan projek ini memiliki beberapa tahapan yang dilakukan, diantaranya melakukan _data cleaning ,missing value,dan reduction data_ . dalam projek ini, hal pertama yang dilakukan adalah melakukan penggabungan **movie.csv** dan **rating.csv** , pemilihan kedua file ini akan berhubungan erat dengan pemilihan metode reekomendasi yang akan dilakukan di projek ini yaitu _user based filtering_ dan _collaborative based filtering_. 


### Data cleaning pada _feature_ title  
seperti yang telah di bahas pada paragraf sebelumnya, dalam projek ini hal pertama yang dilakukan aldah menggabungkan file **movie.csv** dan **rating.csv** yang mana akan menjadi satu variable bernama **films**. seteleh menggabungkan hal pertama yang dapat dilihat dari datasheet kita adanya keanehan dalam feture title ,dalam feture tersebut nama film selalu disertakan dengan tahun rilis. oleh sebab itu , feature _title_disederhankan dengan menghilangkan tahun rilis dan memindahkanya dalam feature baru yang bernama **tahun_rilis** . tujuan dalam melaukan tindakan ini adalah membuat model lebih mudah di pahami dan menghindarkan reduntansi yang terjadi dikarnakan adanya angka dan huruf dalam satu feture yang sama.

### Data cleaning pada _feature_ ratings 

Setelah menyelesaikan data cleaning , pada projek ini hal yang perlu di perhatikan adalah nilai yang ada pada rating . Pada saat pengecekan di temui bahwa skala yang di gunakan dalam rating tidak menggunkana angka bulat, sehingga dalam kasus ini memutuskan untuk mengubah sekala dengan angka bulat untuk memudahkan user mengetahui seberapa bagus film tersebut .

 ### Data cleaning pada _feature_ timestamps 
dalam feature rating terlihat bahwa angka yang tertera sangat sulit di pahami ,dikarenakan untuk mempermudah kita dalam memahami data  kita mengubah angka yang terlihat secara sekilas seperti anka _random_ menjad angka dengan format tahun tanggal dan bulan .  

### Penanganganan _Missing Vlue_
setelah merapikan data dalam _variable **films**_ selanjutnya adalah pengecekan apakah data set memiliki nilai yang lengkapa dan tidak ada nilai uang _null_ dan kosong sehingga dalam kasus ini terdapat nilai kosong yang terdapat dalam dataset diantaranya 

|feature | missing value |
| --- | --- |
|tahun rilis | 17 |
|user Id | 18 |
|rating | 18 |
|time stamp | 18 |

dari tabel diatas ada beberapa feature ynag memiliki nilai kosong atau kosong , sehingga dengan jumlah yang sedikit  berbanding dengan jumlah data   100,0000 rating , 3,600 tag dan 9000 film penangan paling _effisien_  menangani nya dengan cara menghapus data tersebut.
### 




**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.



## Modeling
  Untuk menyelasaikan masalah yang sudah disinggung sebelumnya, pada projek ini solusii yang di tawarkan ada dua yaitu _Content Based Filtering_ dan _ collaborative filtering_. kedua solusi ini memiliki keunggulan dan kelebihan tersendiri.Selanjutnya akan di perlihatkan bagaimamna kedua metode ini dapat menyelesaikan permasalahan yang telah disebutkan sebelumnya.

### Content Based Filtering
metode ini merupakan suau metode yang mempelajari profil minat pengguna baru berdasarkan data dari objek yang telah dinilai pengguna. Algoritma ini bekerja dengan menyarankan item serupa yang pernah disukai di masa lalu atau sedang dilihat di masa kini kepada pengguna. tentunya semakin banyak data semakin bagus pula metode ini.namun tentu sistem ini memiliki kelebihan dan kekurangan diantaranya  : 

**Kelebihan Content-Based Filtering**:
- Personalisasi: Content-Based Filtering dapat memberikan rekomendasi yang sangat personal karena bergantung pada preferensi pengguna yang sudah diketahui. Ini memungkinkan rekomendasi yang cocok dengan minat dan sejarah pengguna.
- Tidak Memerlukan Data Pengguna Lain: Metode ini tidak memerlukan data pengguna lain atau kolaborasi antar pengguna. Ini bermanfaat dalam kasus-kasus di mana data pengguna terbatas atau tidak tersedia sama sekali.
- Transparansi: Model Content-Based Filtering cenderung lebih transparan daripada metode kolaboratif. Anda dapat menjelaskan rekomendasi kepada pengguna dengan merujuk pada fitur-fitur item yang mereka sukai.
- Penanganan Item Baru: Content-Based Filtering dapat menangani item baru dengan baik, bahkan jika tidak ada data kolaboratif. Ini karena rekomendasi didasarkan pada karakteristik item itu sendiri.

Kekurangan Content-Based Filtering:
- Keterbatasan Dalam Rekomendasi Serendah: Content-Based Filtering cenderung membatasi rekomendasi pada item yang serupa dengan yang sudah dikonsumsi oleh pengguna. Ini dapat mengurangi kemungkinan pengguna menemukan konten yang berbeda atau mendapat penawaran yang lebih menarik.
- Keterbatasan dalam Memahami Preferensi Kompleks: Meskipun Content-Based Filtering dapat memahami preferensi berdasarkan fitur-fitur, ia mungkin tidak dapat menangkap preferensi yang lebih kompleks atau bervariasi. Misalnya, ia mungkin kesulitan merekomendasikan item yang berbeda dari biasa pengguna.
- Keterbatasan Data: Kinerja Content-Based Filtering sangat tergantung pada kualitas dan kelengkapan data atribut item. Jika data ini tidak memadai atau tidak lengkap, maka kualitas rekomendasi akan terpengaruh.
- Over-Spesialisasi: Ada risiko bahwa model Content-Based Filtering bisa terlalu spesifik dalam rekomendasi, menghasilkan daftar rekomendasi yang terlalu serupa.
- Kurangnya Diversifikasi: Content-Based Filtering cenderung kurang efektif dalam menghadirkan variasi dalam rekomendasi karena cenderung merekomendasikan item dengan karakteristik yang sama.

### menyiapkan Variable
dalam projek in hal yang pertama kali dilakukakn adalah membuat sebuah variable dari data yang telah kita olah dari tahap _Data preprocessing _ dari sana kita dapa menggunakan command _tolist_ untuk membuat variable bernama _data_.Setelah kita mendapatkan variable , pada projek ini untuk mempermudah pengerjaaan model pertama ,hal pertama dilakukan adalah  mengubah 
 nama variable dari data menjadi _saringan_. 

### TF-IDF Vectorizer
setelah menyiapakan nama variable , pada tahap selanjutnya kita akan menggunakan TF-IDF Vectorizer yang berasal dari library sklearn . dengan menggunakan fungsi TfidfVectorizer() kita dapat menggunakan fitur ini. Setelah menggunkan itu kita mengubah variable  menjadi bentuk matriks .yang mana pada matriks menunjukkan korelasi antara film dengan genre-nya.
![image](https://github.com/RR21-crypto/RECOMENDATION-_SYSTEM/assets/81364035/4abe8d50-4c83-4e60-a835-42b08c8aa68f)




Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan. Sajikan top-N recommendation sebagai output.

 ### Cosine Smiliarity 
 Selanjutnya pada projekk ini akan menggunakan Cosine Smiliarity , yang mana dengan fungsi ini dapat menghitung degree smiliarity anatar judul fim dan korleasi dengan kategori genre yang dimiliki oleh film tersebut.Perhitungan similarity merupakan tahapan paling penting dalam pendekatan content-based filtering, karena pada dasarnya pendekatan ini menerapkan prinsip kesamaan antar item untuk mendapatkan hasil rekomendasi yang sesuai. Output dari cosine similarity akan menghasilkan suatu matrix kesamaan yang bisa dilihat pada konversi ke bentuk dataframe berikut.
 

![cosine smiliarity_1](https://github.com/RR21-crypto/RECOMENDATION-_SYSTEM/assets/81364035/14832e21-25c6-4e91-a726-73ed7e9aef6d)

dari gambar diatas diketahui bentuk matriks yang  dapatkan adalah bentuk 9708 x 9708 dari gambar tersebut tidak hanya bentuk matriks saja yang  dapatkan, namun dapat dilihat kesamaaan anatr film , sperti yang terlihat dari gambar diatas yang di beri kotak berwarna merah bahwa _film_ _George Carlin: Jammin' in New York_ dan film _Oh, God! Book II_ memliliki nilai kesamaan berupa 1.0 . sehingga dapat diartikan bahwa kedua film memiliki kemiripan yang sanagt tinggi bahkan hampir sama berdasarkan genre yang mereka miliki, sehingga model dapat merekomendasikan antara kedua film.

 ### Membuat Function khusus 
 pada tahapan ini , adalah tahapan untuk membuat sebuah fungsi khusus untuk menampilkan sistem rekomendasi yang sudah kita buat pada tahap sebelumnya,dengan menggunkaan funtion ini akan menampilkan rekomendasi bersarkan nilai kemiripan sesuai dengan model yang sudah kita olah sebelumnya. hal yang  pertama dilakukan oleh funtion ini mengambil data yang sudah diolah dengan sesuai range nilai kesamaan  yang telah di _declare_ lalu setelah data masuk  tahapan ini berda dalam _variable closest_, selanjutnya dalam merekemondasikan film ,normalnya namam yang diinginkan oleh user tidak akan tampil dalam daftar rekomendasi yang diinginkan, oleh karena itu sistem akan mendrop hal tersebut. jumlah rekomendasi yang ditampilkan berdasarkan nilai **K** , dalam projek ini nilainya adalah 8 . 
![image](https://github.com/RR21-crypto/RECOMENDATION-_SYSTEM/assets/81364035/45a3533e-9990-4f8a-acae-ee1158cc0ba0)

### Recomendation 
masuk pada tahap akhir dalam metode ini yaitu mendapatkan rekomendasi, dalam projek ini hal pertama yang dilakukan apakah judul yang diinginkan user ada dalam daftar yang kita miliki seperti pada gambar dibawah.

![image](https://github.com/RR21-crypto/RECOMENDATION-_SYSTEM/assets/81364035/95ad70bb-5255-4390-93bf-02d5818604e7)


setelah itu user bisa mengetahui rekomendasi film yang sebelumnya dengan menggunakan function di bawah

 
 
 ![image](https://github.com/RR21-crypto/RECOMENDATION-_SYSTEM/assets/81364035/85253de9-6e20-4cc8-9a4a-b1b4085e7d7a)
 
dapat dilihat model merekomendasikan 8 judul film dengan genre yang sama yaitu genre _comedy_.

## Model Development Dengan Collaborative Filtering

dalam projek ini terdapat beberapa tahap yang dilakuakn untuk mendapatkan hasil yang dibutuhkan ,tentunya sistem ini memmiliki kelebihan dan kekurangan diantaranya: 

kelebihan :
- Rekomendasi Serendah: Collaborative Filtering mampu memberikan rekomendasi yang sangat sesuai dengan preferensi pengguna. Ini berdasarkan kesamaan preferensi dengan pengguna lain yang memiliki sejarah konsumsi serupa.
- Tidak Bergantung pada Informasi Item: Metode ini tidak memerlukan informasi rinci tentang atribut item. Ini berguna ketika Anda memiliki banyak item tanpa informasi deskriptif yang cukup.
- Kemampuan Menangani Perubahan Data: Collaborative Filtering dapat menangani perubahan data dengan baik. Ketika ada penambahan item baru atau perubahan preferensi pengguna, model dapat diperbarui dengan data terbaru.
- Efektif untuk Item Ritel: Metode ini cocok untuk merekomendasikan item ritel, seperti produk e-commerce, film, atau musik, karena preferensi pengguna dapat dengan mudah diperoleh dari perilaku sebelumnya.

kekurangan : 
- Masalah Cold Start: Metode ini cenderung tidak efektif saat menghadapi situasi "cold start" di mana Anda memiliki sedikit atau tidak ada data perilaku pengguna atau item.
- Permasalahan Skalabilitas: Untuk platform besar dengan jutaan pengguna dan item, perhitungan kesamaan dalam Collaborative Filtering bisa menjadi mahal secara komputasi.
- Risiko Over-Spesialisasi: Ada risiko bahwa model Collaborative Filtering akan menjadi terlalu spesifik dalam rekomendasi, terutama jika tidak ada cukup variasi dalam data pelatihan.
- Masalah Privasi: Dalam implementasi nyata, perlu diperhatikan masalah privasi, terutama dalam metode Collaborative Filtering berbasis pengguna, karena data pengguna harus dibagikan atau digunakan untuk menghitung rekomendasi.

tahap akan di jelaskan peroses untuk mendapatkan hasil rekomendasi sebagai berikut :

### Data preparation 
dalam tahap ini data yang kita gunakan adalah dari file _rating.csv_ , data tersebut dimasukan kedalam variable **dd** . selanjutnya variable tersebut akan di olah kembali menjadi sesuai dengan format yang kita butuhkan, mulai dari membulatkan nilai rating  dan mengubah format  timestamp .

### Split Data for Training and Validation

Data dibagi untuk data train dan validasi dengan komposisi 80/20. Pembagian ini bertujuan agar data yang digunakan dapat digunakan untuk mengembangkan model dan mengevaluasi performance dari model yang telah dikembangkan.

### peroses Training 

pada tahap ini , model akan menghitung kecocokan antara pengguna dan resto dengan teknik embedding.peroses ini melakukan teknik perkalian dot product antara judul dan genre dengan skala kecocokan [ 0, 1] dan aktivasi sigmoid., pada proses compile dilakukan menggunakan BinaryCrossentropy untuk menghitung loss function, Adam (Adaptive Moment Estimation) sebagai optimizer, dan root mean squared error (RMSE) sebagai metrics evaluation. Proses training model berjalan sebanyak 100 epochs sebagai berikut. dalam  melakuakn peroses training terdapat fungsi call back untuk menghentikan ketika RMSE kurang dai 0.1 mengingat banyaknya pelatihan  yang dilakukan pada latihan ini , dengan begitu dapat menghemat waktu.

### Visualisasi Metrik
tahap ini di tujukan untuk melihat hasil latihan model yang kita lakukan, dari sini dapat dilihat perbedaan RMSE antara _train dan test_.dengan melihat gambar dibawah di dapati nilai dari RMSE test adalah 0.27 dan untuk train adalah 0.17.

![image](https://github.com/RR21-crypto/RECOMENDATION-_SYSTEM/assets/81364035/eda3f553-2b97-48ef-a905-47fcd9636962)

### mendapatkan rekomendasi Resto 
setelah menyelasaikan semua tahap pelatihan dan preparation selanjutnya adalah tajap untuk melihat hasil rekomendasi yang akan di dapatkan, dengan menggunakan fungsi _model.predict()_ hasil rekomendasi dapat di tampilkan seperti yang ada pada gambar di bawah.
 ![image](https://github.com/RR21-crypto/RECOMENDATION-_SYSTEM/assets/81364035/77304be7-a756-44f1-bb2a-264046423ba2)



## Evaluation
setelah menyelesaikan semua model selajutnya adalah tahap untuk mengevaluasi peforma dari model yang di kembangkan pada projek ini, pada projek ini model menggunakan dua buah metode yang maan akan di evaluasi satu persatu.\
### Evaluasi Content Based filteing 
pada metode ini untuk mengukur performance model diukur menggunakan nilai metriks precisions dengan similarity. cosine smiliarity dapat di hitung secara manual dengan menggunakan rumus yang ada pada gambar di bawah : 

![image](https://github.com/RR21-crypto/RECOMENDATION-_SYSTEM/assets/81364035/1d685c64-3840-4bd0-b419-5cf2dce37948)

setelah itu metrik yang digunakan dapat di ilustrasikan seperti ilustrasi di bawah, dari gambar di bawah dapat nilai dari smiliarity yang  di dapat pada di gambarkan seperti di bawah , dimana semakin besar nilai smiliarity yang dimiliki maka semakin besar sudut yang kita dpatkan dimana nilai _smiliarity_ nya adalah 1 begitu juga sebaliknya. 
![image](https://github.com/RR21-crypto/RECOMENDATION-_SYSTEM/assets/81364035/86599dca-8e81-4da1-8db8-70ccc0cac446)


setelah mengetahui metriks yang di gunakan untuk mengukur precision yang di dapatkan dapat menggunkanan rumus yang ada di bawah :

![image](https://github.com/RR21-crypto/RECOMENDATION-_SYSTEM/assets/81364035/fa79d7ae-94d7-47bb-a4fe-0f41e90c03b8)
lalu lihat film yang ingin di rekomendasikan , disini dalam projek ini user menginginkan rekomendasi dari fillm _Oh, God! Book II_ yang memiliki genre _comedy_ .

![image](https://github.com/RR21-crypto/RECOMENDATION-_SYSTEM/assets/81364035/50c5d506-06c9-4e89-9da8-5b2263d99be1)

setelah itu mari lihat hasil rekomendasi yang di dapatkan user 
![image](https://github.com/RR21-crypto/RECOMENDATION-_SYSTEM/assets/81364035/2b6fe2be-4c6e-4330-af89-a07c99a65a89)

 setelah melihat hasil rekomendasi lalu kita dapat lihat hasil recomendasi mengeluarkan film dengan genre comedy  yang mana adapat di simpulkan bahwa nilai _precision yang kita dapatkan adalah 8/8 atau bisa di sebut 100 persen 





Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
