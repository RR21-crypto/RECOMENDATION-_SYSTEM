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
