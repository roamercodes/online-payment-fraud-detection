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

Berikut informasi dataset:  
- Dataset memiliki 6362620 sampel dan 11 fitur.
- Dataset memili 3 fitur bertipe data object, 3 bertipe data int64 dan 4 bertipe data float64.
- Dataset berformat CSV (comma separated value).

### Variabel-variabel pada dataset adalah sebagai berikut:
- step            : Memetakan satuan waktu di dunia nyata. Dalam hal ini 1 step adalah 1 jam. Total step 744 (simulasi 30 hari).
- type            : Metode transaksi 
- amount          : Jumlah transaksi
- nameOrig        : Pelanggan memulai transaksi
- oldbalanceOrg   : Saldo awal sebelum transaksi
- newbalanceOrig  : Saldo baru setelah transaksi
- nameDest        : Penerima transaksi
- oldbalanceDest  : Penerima saldo awal sebelum transaksi.
- newbalanceDest  : Penerima saldo baru setelah transaksi.
- isFraud         : Transaksi penipuan.
- isFlaggedFraud  : Transaksi ditandai penipuan dan melibatkan transfer lebih dari 200.000 unit dalam mata uang tertentu.

### Penanganan missing value & Outliers

Pada gambar dibawah ini dapat diketahui bahwa tidak ada _missing value_ pada setiap fitur.

![image](https://github.com/roamercodes/online-payment-fraud-detection/assets/22432578/694fc23e-cda5-4d06-a066-48dc8b3abc1b)

Distrusi sebaran data pada masing-masing fitur numerik.


Step

![image](https://github.com/roamercodes/online-payment-fraud-detection/assets/22432578/f574ebfd-5dd4-4881-8cac-0664e72c5268)

Amount
![image](https://github.com/roamercodes/online-payment-fraud-detection/assets/22432578/d4b10f3e-acb2-43dd-8dbf-bfcfe54c4364)

OldBalanceOrg
![image](https://github.com/roamercodes/online-payment-fraud-detection/assets/22432578/3e0e4bf5-e91a-4d6e-96c1-0703bfc315f5)
NewBalanceOrig
![image](https://github.com/roamercodes/online-payment-fraud-detection/assets/22432578/7c98fecf-ba47-44ea-82bb-c888aae2c65a)
OldBalanceDest
![image](https://github.com/roamercodes/online-payment-fraud-detection/assets/22432578/c46585a4-ee91-478f-884c-55aa1b13f03e)
NewBalanceDest
![image](https://github.com/roamercodes/online-payment-fraud-detection/assets/22432578/b56b7dfe-2284-4f33-9258-59a2d154b244)

Untuk menghapus _outliers_ akan digunakan metode IQR.
IQR adalah singkatan dari Inter Quartile Range. Kuartil dari suatu populasi adalah tiga nilai yang membagi distribusi data menjadi empat sebaran. Seperempat dari data berada di bawah kuartil pertama (Q1), setengah dari data berada di bawah kuartil kedua (Q2), dan tiga perempat dari data berada di kuartil ketiga (Q3). Dengan demikian interquartile range atau IQR = Q3 - Q1.

Distribusi sebaran data setelah _outliers_ dibersihkan.


Step
![image](https://github.com/roamercodes/online-payment-fraud-detection/assets/22432578/2b8806f6-3cac-4f51-8dfd-b004d8e4458f)
Amount
![image](https://github.com/roamercodes/online-payment-fraud-detection/assets/22432578/138a8920-2c0e-47e7-993f-8db7bf9a4b35)
OldBalanceOrg
![image](https://github.com/roamercodes/online-payment-fraud-detection/assets/22432578/9195630d-977c-4307-89af-bacf6f6e86d4)
NewBalanceOrig
![image](https://github.com/roamercodes/online-payment-fraud-detection/assets/22432578/6127d3ed-baef-43c1-a63c-683e943ef026)
OldBalanceDest
![image](https://github.com/roamercodes/online-payment-fraud-detection/assets/22432578/ce4b71b5-0142-40f5-a04f-dad397972de9)
NewBalanceDest
![image](https://github.com/roamercodes/online-payment-fraud-detection/assets/22432578/bc110d45-7a84-42bf-84bc-2f50d3377c00)



### Univariate Analysis
Analisis univariat merupaka teknik analisis data terhadap satu variabel secara mandiri.

Kita akan melihat ada metode transaksi apa saja pada kumpulan data ini yang ada pada fitur type, ternyata pada fitur type ada lima jenis metode transaksi, yaitu:
- Payment
- Transfer
- Cash Out
- Debit
- Cash in

Sebaran data fitur _type_ metode transaksi _cash_out_ menjadi yang tertinggi sebanyak 35% dan _debit_ menjadi yang terkecil yakni 0.7%.

![image](https://github.com/roamercodes/online-payment-fraud-detection/assets/22432578/d0b63e2e-0df0-4683-9151-c7eeb78ad8f8)


Pada fitur isFraud berisi _boolean_ label target yakni 0 dan 1, ada 6354407 untuk label 0 dan 8213 untuk label 1 yang berarti ada 8213 ditandai sebagai transaksi penipuan. Jika dilihat dari total data maka untuk transaksi yang ditandai penipuan hanya 0.13%

![image](https://github.com/roamercodes/online-payment-fraud-detection/assets/22432578/b7198d14-b83f-4626-995d-f5475eca532d)

Kemudian pada kolom _isFraud_ transaksi penipuan hanya terjadi di 2 metode transaksi, yakni _cash_out_ dan _transfer_

![image](https://github.com/roamercodes/online-payment-fraud-detection/assets/22432578/cfff1136-ffb9-4dff-9983-5f6358a67150)

Pada kolom _isFlaggedFraud_ ada 16 transaksi yang ditandai sebagai penipuan melibatkan transfer lebih dari 200.000 unit dalam mata uang tertentu. Karena terlalu sedikit, maka fitur tersebut tidak akan digunakan.

![image](https://github.com/roamercodes/online-payment-fraud-detection/assets/22432578/4d993b27-a80d-4910-b4ff-63a2b24a6c75)




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

