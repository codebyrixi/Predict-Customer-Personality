# Predict Customer Personality to Boost Marketing Campaign by Using Machine Learning
Project ini merupakan project yang bertujuan untuk melakukan pediksi perilaku pelanggan guna meningkatkan campaign marketing di suatu perusahaan. Project ini dibuat menggunakan bahasa pemrograman Python

## Daftar Isi
- Analisis Tingkat Konversi Berdasarkan Pendapatan, Pengeluaran dan Usia
- Data Cleaning and Preprocessing
- Feature Engineering
- Data Modelling
- Analisis Kepribadian Pelanggan Untuk Penargetan Ulang Pemasaran

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
<p align="center">
  <img src="https://github.com/user-attachments/assets/288c8a0e-6207-4a9e-8c60-32210d2b637f"/>
</p>
Dapat dilihat pada plot <i>distortion score</i> diatas, bahwa jumlah cluster terbaik yang ditemukan berdasarkan hasil analisis adalah 4 dengan skor 4864.63. Algoritma K-means digunakan untuk mengelompokkan data setelah menentukan jumlah cluster yang ideal sebelumnya. Algoritma ini mengelompokkan data berdasarkan kesamaan fitur, memungkinkan untuk mengidentifikasi pola atau kelompok yang ada dalam data dan memahami karakteristik setiap cluster.
<p align="center">
  <img src="https://github.com/user-attachments/assets/070968e2-93ec-4750-b562-70f96869b85e"/>
</p>
Gambar diatas merupakan hasil <i>clustering</i> dengan menggunakan <i>K-Means</i>, dimana plot tersebut menunjukkan bahwa cluster-cluster terbentuk dengan baik dan mengelompokkan data ke dalam beberapa kelompok berbeda. Ini menunjukkan bahwa algoritma clustering berhasil membedakan dan menggolongkan data berdasarkan ciri-cirinya.<br>
Selanjutnya dilakukan tahap evaluasi hasil model. Dengan menggunakan metode Silhouette Score, diberikan rekomendasi bahwa jumlah cluster terbaik adalah 4.
<p align="center">
  <img src="https://github.com/user-attachments/assets/c5357727-4f5b-49e1-9898-e42b4f99487e"/>
</p>
Hal tersebut didasarkan pada fakta bahwa nilai Silhouette Score tertinggi pada jumlah cluster tersebut, yaitu 0,535. Nilai ini merupakan metrik yang menunjukkan seberapa baik objek dalam satu cluster berada dalam kumpulan data mereka sendiri dibandingkan dengan objek dalam cluster lain. Semakin tinggi nilai Silhouette Score, semakin baik cluster-cluster tersebut terpisah.

## Bagian 5: Analisis Kepribadian Pelanggan Untuk Penargetan Ulang Pemasaran
<p align="center">
  <img src="https://github.com/user-attachments/assets/ade9ace0-8265-4972-a8aa-be6a2aa9efcc"/>
</p>
Menurut plot korelasi antara pendapatan dan total pengeluaran, terlihat bahwa terbentuk kelompok yang dapat dibedakan. Dalam kasus ini, cluster 0 dan 3 cenderung berada dalam satu kelompok, yang menunjukkan adanya persamaan dan perbedaan karakteristik di antara mereka. Ketika dua cluster berada dalam satu kelompok, itu menunjukkan bahwa pola pendapatan dan pengeluaran anggota cluster tersebut serupa atau terkait. Tingkat pendapatan dan pengeluaran kedua cluster mungkin sebanding, atau mereka mungkin memiliki tren yang sama.
<p align="center">
  <img src="https://github.com/user-attachments/assets/a80a75ee-df9a-4ff4-9e97-5e95291a45be"/>
</p>
Berdasarkan plot persentase ppulasi cluster diatas, ditemukan bahwa sekitar 50% dari populasi termasuk dalam kelompok Low Customer. Meskipun kelompok ini memiliki angka transaksi dan pengeluaran yang rendah, namun karena populasi mereka yang besar, perusahaan dapat fokus untuk menarik perhatian mereka.<br>
Sedangkan populasi High Customer A dan B cenderung rendah, namun memiliki potensi transaksi, spending, konversi, dan income yang tinggi. Perusahaan dapat mempertimbangkan strategi pemasaran yang lebih personal dan eksklusif untuk menarik minat mereka.
<p align="center">
  <img src="https://github.com/user-attachments/assets/0ce4431d-4f45-4597-99de-8011982d183f"/>
</p>
Berikut ini ditampilkan plot karakteristik mayoritas/rata-rata total transaksi, pengeluaran, pendapatan, recency, dan conversion rate berdasarkan clusternya. Terlihat pada grafik tersebut, bahwa dapat diketahui karakteristik dari tiap cluster berdasar pola transaksi pelanggan dan dapat dikelompokkan berdasarkan kategori berikut.
<p align="center">
  <img src="https://github.com/user-attachments/assets/c50716e8-63c5-4cb1-8744-a4d51bf13b52"/>
</p>
Dari karakteriktik tersebut, dapat setiap cluster dapat dikelompok berdasarkan kategori, yaitu sebagai berikut.
| Nama Cluster |                 Jenis Kategori                 |   Nama Kategori   |
|:------------:|:----------------------------------------------:|:-----------------:|
|   Cluster 0  |     _High-Transaction High-Spending Group_     |  High Customer A  |
|   Cluster 1  |      _Low-Transaction Low-Spending Group_      |    Low Customer   |
|   Cluster 2  |       _High-Income High-Conversion Group_      |  High Customer B  |
|   Cluster 3  | _Moderate-Transaction Moderate-Spending Group_ | Moderate Customer |
