# Laporan Proyek Machine Learning - Muhammad Kholilullah

## Domain Proyek

### Latar Belakang 

Perkembangan teknologi yang begitu pesat memberi dampak luar biasa kehidupan sehari-hari disertai aktivitas bertransaksi secara elektronik yang menawarkan kemudahan dalam prosesnya. Tetapi disisi lain juga terjadi transaksi penipuan yang beragam caranya. Keberagaman jenis transaksi penipuan yang dilakukan menyebabkan sulitnya mengidentifikasi transaksi penipuan yang tentu saja dapat merugikan pehiak terkait. Tujuan penelitian ini adalah membuat model terbaik yang dapat mendeteksi adanya transaksi penipuan dengan machine learning menggunakan metode klasifikasi beberapa algoritmanya.  

Pada bagian ini, kamu perlu menuliskan latar belakang yang relevan dengan proyek yang diangkat.

**Referensi**:
- [Mengenal Elektronik Banking](http://ejurnal.ppsdmmigas.esdm.go.id/sp/index.php/swarapatra/article/view/125/112) 
- [Penerapan Deep Learningdalam Deteksi Penipuan Transaksi Keuangan Secara Elektronik](https://ejurnal.teknokrat.ac.id/index.php/teknoinfo/article/view/868/517) 
- [Analisa Transaksi Belanja Online Pada Masa Pandemi Covid-19](https://ejurnal.teknokrat.ac.id/index.php/teknoinfo/article/view/868/517) 
  
## Business Understanding

Pada bagian ini, kamu perlu menjelaskan proses klarifikasi masalah.

Transaksi penipuan yang terjadi saat ini telah menggunakan sistem secara elektronik sehingga untuk mengidentifikasi tersebut perlu juga menggunakan teknologi yang mumpuni. Teknologi machine learning dapat berkontribusi secara bermanfaat dalam tantangan mendeteksi transaksi penipuan.

Bagian laporan ini mencakup:

### Problem Statements

Menjelaskan pernyataan masalah latar belakang:
- Fitur apa yang paling berpengaruh terhadap transaksi penipuan?
- Pada jenis pembayaran apa transaksi penipuan sering terjadi?
- Pernyataan Masalah n

### Goals

Menjelaskan tujuan dari pernyataan masalah:
- Mengetahui fitur yang paling berkorelasi terhadap transaksi penipuan
- Mengetahui pada metode pembayaran apa transaksi penipuan sering terjadi
- 

Semua poin di atas harus diuraikan dengan jelas. Anda bebas menuliskan berapa pernyataan masalah dan juga goals yang diinginkan.

### Solution Statement
- Model klasifikasi yang yaitu SVM, KNN dan Random Forest


Menjelaskan tujuan dari pernyataan masalah:
- Mengetahui fitur yang paling berkorelasi terhadap transaksi penipuan
- Mengetahui pada metode pembayaran apa transaksi penipuan sering terjadi

**Rubrik/Kriteria Tambahan (Opsional)**:
- Menambahkan bagian “Solution Statement” yang menguraikan cara untuk meraih goals. Bagian ini dibuat dengan ketentuan sebagai berikut: 

    ### Solution statements
    - Mengajukan 2 atau lebih solution statement. Misalnya, menggunakan dua atau lebih algoritma untuk mencapai solusi yang diinginkan atau melakukan improvement pada baseline model dengan hyperparameter tuning.
    - Solusi yang diberikan harus dapat terukur dengan metrik evaluasi.

## Data Understanding
Paragraf awal bagian ini menjelaskan informasi mengenai data yang Anda gunakan dalam proyek. Sertakan juga sumber atau tautan untuk mengunduh dataset. Contoh: [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Restaurant+%26+consumer+data).

Data yang digunakan dalam proyek ini didapatkan di situs [kaggle](https://kaggle.com) kumpulan data ini merupakan data sintetik yang dihasilkan menggunakan simulator yang dimanakan PaySim. PaySim mensimulasikan transaksi elektronik berdasarkan sampel transaksi nyata yang diambil dari log transaksi keuangan satu bulan dari layanan uang seluler yang diterapkan di negara Afrika. Lebih lebih detailnya bisa dilihat pada sumber data [kaggle: online fraud detection](https://www.kaggle.com/datasets/jainilcoder/online-payment-fraud-detection?resource=download)

Selanjutnya uraikanlah seluruh variabel atau fitur pada data. Sebagai contoh:  

### Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
- step : memetakan satuan waktu di dunia nyata. Dalam hal ini 1 langkah adalah 1 jam waktu. Total langkah 744 (simulasi 30 hari).
- type : Metode transaksi 
- dst


Ini adalah contoh 1 baris dengan penjelasan header:

1, PEMBAYARAN,1060.31,C429214117,1089.0,28.69,M1591654462,0.0,0.0,0,0


jumlah -
jumlah transaksi dalam mata uang lokal.

nameOrig - pelanggan yang memulai transaksi

oldbalanceOrg - saldo awal sebelum transaksi

newbalanceOrig - saldo baru setelah transaksi

nameDest - pelanggan yang menjadi penerima transaksi

oldbalanceDest - penerima saldo awal sebelum transaksi. Perhatikan bahwa tidak ada informasi untuk pelanggan yang dimulai dengan M (Merchants).

newbalanceDest - penerima saldo baru setelah transaksi. Perhatikan bahwa tidak ada informasi untuk pelanggan yang dimulai dengan M (Merchants).

isFraud - Ini adalah transaksi yang dilakukan oleh agen penipuan di dalam simulasi. Dalam kumpulan data khusus ini perilaku penipuan agen bertujuan untuk mendapatkan keuntungan dengan mengambil kendali atau akun pelanggan dan mencoba mengosongkan dana dengan mentransfer ke akun lain dan kemudian menguangkan sistem.

isFlaggedFraud - Model bisnis ini bertujuan untuk mengontrol transfer besar-besaran dari satu akun ke akun lain dan menandai upaya ilegal. Upaya ilegal dalam kumpulan data ini adalah upaya untuk mentransfer lebih dari 200.000 dalam satu transaksi.



Selanjutnya uraikanlah seluruh variabel atau fitur pada data. Sebagai contoh:  

### Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
- accepts : merupakan jenis pembayaran yang diterima pada restoran tertentu.
- cuisine : merupakan jenis masakan yang disajikan pada restoran.
- dst

**Rubrik/Kriteria Tambahan (Opsional)**:
- Melakukan beberapa tahapan yang diperlukan untuk memahami data, contohnya teknik visualisasi data atau exploratory data analysis.

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahapan ini membahas mengenai model machine learning yang digunakan untuk menyelesaikan permasalahan. Anda perlu menjelaskan tahapan dan parameter yang digunakan pada proses pemodelan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan kelebihan dan kekurangan dari setiap algoritma yang digunakan.
- Jika menggunakan satu algoritma pada solution statement, lakukan proses improvement terhadap model dengan hyperparameter tuning. **Jelaskan proses improvement yang dilakukan**.
- Jika menggunakan dua atau lebih algoritma pada solution statement, maka pilih model terbaik sebagai solusi. **Jelaskan mengapa memilih model tersebut sebagai model terbaik**.

## Evaluation
Pada bagian ini anda perlu menyebutkan metrik evaluasi yang digunakan. Lalu anda perlu menjelaskan hasil proyek berdasarkan metrik evaluasi yang digunakan.

Sebagai contoh, Anda memiih kasus klasifikasi dan menggunakan metrik **akurasi, precision, recall, dan F1 score**. Jelaskan mengenai beberapa hal berikut:
- Penjelasan mengenai metrik yang digunakan
- Menjelaskan hasil proyek berdasarkan metrik evaluasi

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.

