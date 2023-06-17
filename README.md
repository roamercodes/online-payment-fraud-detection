# Laporan Proyek Machine Learning - Muhammad Kholilullah

## Domain Proyek

### Latar Belakang 

Perkembangan teknologi yang begitu pesat memberi dampak luar biasa kehidupan sehari-hari disertai aktivitas bertransaksi secara elektronik yang menawarkan kemudahan dalam prosesnya. Tetapi disisi lain juga terjadi transaksi penipuan yang beragam caranya. Keberagaman jenis transaksi penipuan yang dilakukan menyebabkan sulitnya mengidentifikasi transaksi penipuan yang tentu saja dapat merugikan pehiak terkait. Tujuan penelitian ini adalah membuat model terbaik yang dapat mendeteksi adanya transaksi penipuan dengan machine learning menggunakan metode klasifikasi beberapa algoritmanya.  

**Referensi**:
- [Applying Supervised Machine Learning Algorithms for Fraud Detection in Anti-Money Laundering](https://hcommons.org/deposits/objects/hc:43350/datastreams/CONTENT/content) 
- [Advantages of the PaySim Simulator for Improving Financial Fraud Controls](https://ntnuopen.ntnu.no/ntnu-xmlui/bitstream/handle/11250/2640900/Computing2019papercameraready.pdf?sequence=1) 
- [Mengenal Elektronik Banking](http://ejurnal.ppsdmmigas.esdm.go.id/sp/index.php/swarapatra/article/view/125/112) 
- [Penerapan Deep Learningdalam Deteksi Penipuan Transaksi Keuangan Secara Elektronik](https://ejurnal.teknokrat.ac.id/index.php/teknoinfo/article/view/868/517) 
- [Analisa Transaksi Belanja Online Pada Masa Pandemi Covid-19](https://ejurnal.teknokrat.ac.id/index.php/teknoinfo/article/view/868/517) 
- [dicoding - machine learning terapan](https://www.dicoding.com/academies/319)
  
## Business Understanding

Transaksi penipuan yang terjadi saat ini telah menggunakan sistem secara elektronik sehingga untuk mengidentifikasi tersebut perlu juga menggunakan teknologi yang mumpuni. Teknologi machine learning dapat berkontribusi secara bermanfaat dalam tantangan mendeteksi transaksi penipuan.

### Problem Statements

- Fitur apa yang paling berpengaruh terhadap transaksi penipuan?
- Pada jenis pembayaran apa transaksi penipuan sering terjadi?
- Pernyataan Masalah n

### Goals

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

### Multivariate Analysis

- Korelasi antar fitur numerik
![image](https://github.com/roamercodes/online-payment-fraud-detection/assets/22432578/1fbbe7b9-d309-4603-b6eb-e6f0659884e1)

  _newbalanceOrig_ dan _oldbalanceOrg_ meliki korelasi yang tinggi.
  _newbalanceDest_ dan _oldbalanceDest_ juga memiliki korelasi tinggi.

Selain itu, kami memiliki korelasi yang relatif tinggi antara jumlah dan newbalanceDest dan jumlah dengan oldbalanceDes

## Data Preparation

![image](https://github.com/roamercodes/online-payment-fraud-detection/assets/22432578/00dda550-c83c-4b38-9549-28680ccd4088)

Seperti pada gambar diatas, fitur pada kolom _type_ masih bertipe objek, agar dapat diolah oleh algorima maka perlu dilakukan perubahan menjadi numerik.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Merubah


- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Model algoritma pada penelitian ini menggunakan 3 model algoritma, yaitu [Logistic Regression](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html) [Random Forest](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html) [XGBoost](https://xgboost.readthedocs.io/en/stable/).

- Logistic Regression
  Regresi logistik adalah teknik analisis data yang menggunakan matematika untuk menemukan hubungan antara dua faktor data. Kemudian menggunakan hubungan ini untuk memprediksi nilai dari salah satu faktor tersebut berdasarkan faktor yang lain. Prediksi biasanya memiliki jumlah hasil yang terbatas, seperti ya atau tidak. Logistic Regression menggunakan probabilitas untuk memprediksi klasifikasi data kategorikal. Nilai input dapat digabungkan secara linier menggunakan fungsi sigmoid atau logistik dan nilai koefisien untuk memprediksi hasil. Estimasi kemungkinan maksimum dianggap menggunakan fungsi sigmoid untuk mengasumsikan data yang paling mungkin dan probabilitas diberikan antara 0 sampai 1 mengatakan apakah suatu peristiwa akan terjadi atau tidak [Komparasi Support Vector Machine, Logistic Regression Dan Artificial Neural Network dalam Prediksi Penyakit Jantung](https://jurnal.untan.ac.id/index.php/jepin/article/view/48053/75676591338). 
  
  - Kelebihan
    
    Regression models logistik tidak hanya model klasifikasi, tetapi juga memberikan probabilitas. Ini adalah keuntungan besar dibandingkan model yang hanya dapat memberikan klasifikasi akhir. Mengetahui bahwa sebuah instance memiliki probabilitas 99% untuk suatu kelas dibandingkan dengan 51% membuat perbedaan besar. [Logistic Regression](https://interpretable-ml.keamanansiber.id/logistic.html)
  - Kelemahan
    
    Regression models logistik memiliki kelemahan interpretasinya lebih sulit karena interpretasi bobotnya bersifat perkalian dan tidak aditif. Logistic regression dapat mengalami pemisahan lengkap. Jika ada fitur yang akan memisahkan kedua kelas secara sempurna, regression models logistik tidak dapat lagi dilatih. Ini karena bobot untuk fitur itu tidak akan konvergen, karena bobot optimalnya tidak terbatas. Ini benar-benar agak disayangkan, karena fitur seperti itu sangat berguna. Tetapi Anda tidak memerlukan machine learning jika Anda memiliki aturan sederhana yang memisahkan kedua kelas. Masalah pemisahan lengkap dapat diselesaikan dengan memperkenalkan penalty bobot atau mendefinisikan distribusi probabilitas bobot sebelumnya. [Logistic Regression](https://interpretable-ml.keamanansiber.id/logistic.html)
    
- Random Forest

  Random
  
  - Kelebihan
  
    - Menghasilkan eror yang lebih rendah.
    - Memberikan hasil yang bagus dalam klasifikasi.
    - Dapat mengatasi data training dalam jumlah sangat besar secara efisien.
    - Metode yang efektif untuk mengestimasi hilangnya data.
    - Dapat memperkiraan variabel apa yang penting dalam klasifikasi.
    - Menyediakan metode eksperimental untuk mendeteksi interaksi variabel.
  
  - Kekurangan 

    - Waktu pemrosesan yang lama karena menggunakan data yang banyak dan membangun model tree yang banyak pula untuk membentuk random trees karena menggunakan single processor.
    - Interpretasi yang sulit dan membutuhkan mode penyetelan yang tepat untuk data.
    - ketika digunakan untuk regresi, mereka tidak dapat memprediksi di luar kisaran dalam data percobaan, hal ini di mungkinkan data terlalu cocok dengan kumpulan data pengganggu (noisy).
    
- XGBoost

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

