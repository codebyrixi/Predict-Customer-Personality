# Predict Customer Personality to Boost Marketing Campaign by Using Machine Learning
Project ini merupakan project yang bertujuan untuk melakukan pediksi perilaku pelanggan guna meningkatkan campaign marketing di suatu perusahaan. Project ini dibuat menggunakan bahasa pemrograman Python

## Daftar Isi
- Analisis Tingkat Konversi Berdasarkan Pendapatan, Pengeluaran dan Usia
- Data Cleaning, Preprocessing, dan Feature Engineering
- Data Modelling
- Analisis Kepribadian Pelanggan Untuk Retargeting Pemasaran

## Bagian 0: Pendahuluan
Sebuah perusahaan dapat berkembang dengan pesat saat mengetahui customer personality nya, sehingga dapat memberikan layanan serta manfaat lebih baik kepada pelanggan yang berpotensi menjadi pelanggan yang loyal. Dengan mengolah data historis marketing campaign, dapat menaikkan performa dan menyasar pelanggan yang tepat agar dapat bertransaksi di platform perusahaan. Dari insight data tersebut, difokuskan membuat sebuah model prediksi kluster sehingga memudahkan perusahaan dalam membuat keputusan.

## Bagian 1: Analisis Tingkat Konversi Berdasarkan Pendapatan, Pengeluaran dan Usia
<p align="center">
  <img src="https://github.com/user-attachments/assets/0e57dd7d-d007-4cd5-bb4b-92210f600731"/>
</p>
Gambar diatas merupakan plot korelasi conversion rate dengan pendapatan, total pengeluaran, serta usia. Hasil penelitian menunjukkan korelasi positif yang signifikan antara pendapatan dan total pengeluaran terhadap tingkat konversi. Ini menunjukkan bahwa semakin besar pendapatan dan pengeluaran total seseorang, semakin besar kemungkinan mereka akan melakukan pembelian.
<p align="center">
  <img src="https://github.com/user-attachments/assets/704d380f-b3a5-4795-9ced-f311ed78cd15"/>
</p>
Dapat dilihat pada plot regresi dengan pendapatan dan total pengeluaran berikut, bahwa adanya korelasi positif yang kuat antara pendapatan dan pengeluaran total, yang menunjukkan hubungan yang signifikan antara tingkat pendapatan dan pola pengeluaran; dengan demikian, semakin tinggi pendapatan seseorang, semakin besar kemungkinan mereka mengeluarkan lebih banyak uang. Dalam dunia bisnis, pemahaman seperti ini dapat membantu bisnis memahami segmen pelanggan yang memiliki potensi pembelian yang lebih besar dan membuat strategi pemasaran yang tepat untuk meningkatkan keterlibatan dan kepuasan pelanggan.

## Bagian 2: Data Cleaning, Preprocessing
Pada proses ini dilakukan pemrosesan data sekaligus pembersihan data, yang terdiri dari pemeriksaan null / missing value pada data, duplikasi data, tipe data dan konsistensi nilai, serta outlier atau data yang tidak biasa. Hasilnya tertera pada tabel dibawah.<br>
| Asesmen Data      | Temuan                                                                                                   | Penyelesaian                            |
|-------------------|----------------------------------------------------------------------------------------------------------|-----------------------------------------|
| Null Values       | Tidak terdapat null values                                                                               | -                                       |
| Duplicate Values  | Tidak terdapat duplicate values                                                                          | -                                       |
| Konsistensi Nilai | Tipe data `dt_customer` sebaiknya datetime                                                               | Mengubah tipe data nya menjadi datetime |
| Nilai Anomali     | Keseluruhan fitur memiliki outlier. Terlihat juga fitur `income` dan `year_birth` memiliki nilai ekstrim | Handling outlier menggunakan IQR.       |

## Bagian 3: Feature Engineering
Pada tahapan ini, dilakukan pembuatan fitur baru berdasar fitur yang telah ada, bertujuan untuk membuat analisis menjadi lebih bermakna. Fitur baru ini dapat memberi informasi tambahan dengan menggabungkan beberapa fitur yang saling berhubungan untuk membentuk fitur yang lebih baik. Selengkapnya dapat dilihat pada tabel dibawah<br>
| Nama fitur baru         | Sumber                                                                        |
|-------------------------|-------------------------------------------------------------------------------|
| membership_duration     | 2023 - dt_customer                                                            |
| age_categories          | age                                                                           |
| total_children          | kidhome + teenhome                                                            |
| total_transaction       | numdealspurchases + numwebpurchases + numcatalogpurchases + numstorepurchases |
| total_spending          | mntcoke + mntfruits + mntmeatproducts + mntfishproducts + mntsweet            |
| total_accepted_campaign | acceptedcmp1 + acceptedcmp2 + acceptedcmp3 + acceptedcmp4 + acceptedcmp5      |
| cvr                     | total_transaction x numwebvisitsmonth/100                                     |

## Bagian 4: Data Modelling
Setelah mempersiapkan data, selanjutnya dilakukan pre-processing pada data, yaitu:
1. Menghapus fitur yang tidak diperlukan untuk model agar data lebih terfokus.
2. Melakukan encoding pada fitur kategorikal akan agar dapat diolah oleh machine learning.
3. Melakukan standardisasi fitur untuk memastikan skala data seragam dan menghindari bias dalam model.
<p>Setelah dilakukannya pre-processing pada data, tahap berikutnya adalah penggunaan metode Principal Component Analysis (PCA) yang berfungsi mengurangi dimensi data dengan mempertahankan informasi penting. Mereka dapat mengatasi masalah multikolinearitas antar fitur dan mengoptimalkan kinerja model dengan mengurangi dimensi data. Menentukan jumlah cluster terbaik juga merupakan langkah penting dalam proses ini. Analisis ini memilih jumlah cluster yang ideal dengan menggunakan Distortion Score dan Elbow Method. Jumlah cluster terbaik yang ditemukan berdasarkan hasil analisis adalah 4.


## Bagian 5: Analisis Kepribadian Pelanggan Untuk Retargeting Pemasaran
