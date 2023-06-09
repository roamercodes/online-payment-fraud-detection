# Laporan Proyek Machine Learning - Muhammad Kholilullah

## Domain Proyek

### Latar Belakang 

Perkembangan teknologi yang begitu pesat memberi dampak luar biasa kehidupan sehari-hari disertai aktivitas bertransaksi secara elektronik yang menawarkan kemudahan dalam prosesnya [1][6]. Tetapi disisi lain juga terjadi transaksi penipuan yang beragam caranya. Keberagaman jenis transaksi penipuan yang dilakukan menyebabkan sulitnya mengidentifikasi transaksi penipuan yang tentu saja dapat merugikan pihak terkait [2]. Transaksi penipuan secara _online_ pasti terdapat korban yang dirugikan dan pihak lainnya yang diuntungkan, yang dirugikan dapat berupa individu maupun kelompok atau bahkan negara [3][7], Transaksi penipuan telah menimbulkan pengaruh negatif terhadap bidang perekonomian dan bisnis yaitu, merongrong sektor bisnis swasta yang sah, merongrong integritas pasar-pasar keuangan, mengakibatkan hilangnya kendali pemerintah terhadap kebijakan ekonominya, dan timbulnya distorsi dan ketidakstabilan ekonomi [4][8]. Tujuan penelitian ini adalah membuat model terbaik yang dapat mendeteksi adanya transaksi penipuan dengan _machine learning_ menggunakan metode klasifikasi dan beberapa algoritmanya.  

gambar 1. proyek cover

![dataset-cover](https://github.com/roamercodes/online-payment-fraud-detection/assets/22432578/d10751f1-3a25-4b40-9c80-503a67264363)

## Business Understanding

Transaksi penipuan yang terjadi saat ini telah menggunakan sistem secara elektronik sehingga untuk mengidentifikasi tersebut perlu juga menggunakan teknologi yang mumpuni. Teknologi _machine learning_ dapat berkontribusi secara bermanfaat dalam tantangan mendeteksi transaksi penipuan.

### Problem Statements

- Fitur apa yang paling berpengaruh terhadap transaksi penipuan?
- Pada jenis pembayaran apa saja transaksi penipuan sering terjadi?
- Bagaimana cara memprediksi transaksi penipuan?

### Goals

- Mengetahui fitur yang paling berkorelasi terhadap transaksi penipuan.
- Mengetahui pada metode pembayaran apa transaksi penipuan sering terjadi.
- Membuat model _machine learning_ yang dapat memprediksi transaksi penipuan.

### Solution Statement

- Menggunakan 3 model algoritma berbeda yaitu Random Forest, Logistic Regression dan XGBoost.
- Menganalisis dan memvisualisasi set data dengan melakukan analisis univariat dan multivariat untuk memahami data.
- Mengevaluasi akurasi data latih dan data uji lalu mengkomparasikan dengan masing-masing model.
- Menggunakan metrik konfusi sebagai acuan hasil evaluasi untuk mendapatkan kinerja model terbaik.

## Data Understanding

Data yang digunakan dalam proyek ini didapatkan di situs [kaggle](https://kaggle.com) kumpulan data ini merupakan data sintetik yang dihasilkan menggunakan simulator yang dinama+kan _PaySim_. _PaySim_ mensimulasikan transaksi elektronik berdasarkan sampel transaksi nyata yang diambil dari log transaksi keuangan satu bulan dari layanan uang seluler yang diterapkan di negara Afrika. Lebih lebih detailnya bisa dilihat pada sumber data [kaggle: online fraud detection](https://www.kaggle.com/datasets/jainilcoder/online-payment-fraud-detection?resource=download)

Berikut informasi dataset:  

- Dataset memiliki 6362620 sampel dan 11 fitur.
- Dataset memili 3 fitur bertipe data object, 3 bertipe data int64 dan 4 bertipe data float64.
- Dataset berformat CSV (comma separated value).

### Variabel-variabel pada dataset adalah sebagai berikut:

Tabel 1. Deskripsi variabel

| Variabel        | Deksripsi |
| --------------- | ---- |
| step            | Memetakan satuan waktu di dunia nyata. Dalam hal ini 1 step adalah 1 jam. Total step 744 (simulasi 30 hari) |
| type            | Metode transaksi |
| amount          | Jumlah transaksi |
| nameOrig        | Pelanggan memulai transaksi |
| oldbalanceOrg   | Saldo awal sebelum transaksi |
| newbalanceOrig  | Saldo baru setelah transaksi |
| nameDest        | Penerima transaksi |
| oldbalanceDest  | Penerima saldo awal sebelum transaksi |
| newbalanceDest  | Penerima saldo baru setelah transaksi |
| isFraud         | Transaksi penipuan |
| isFlaggedFraud  | Transaksi ditandai penipuan dan melibatkan transfer lebih dari 200.000 unit dalam mata uang tertentu |

### Penanganan missing value & Outliers

Pada tabel dibawah ini dapat diketahui bahwa tidak ada _missing value_ pada setiap fitur.

Tabel 2. jumlah _missing value_

| Variabel        | Missing value |
| --------------- | - |
| step            | 0 |
| type            | 0 |
| amount          | 0 |
| nameOrig        | 0 |
| oldbalanceOrg   | 0 |
| newbalanceOrig  | 0 |
| nameDest        | 0 |
| oldbalanceDest  | 0 |
| newbalanceDest  | 0 |
| isFraud         | 0 |
| isFlaggedFraud  | 0 |


### Univariate Analysis
Analisis univariat merupaka teknik analisis data terhadap satu variabel secara mandiri.

Kita akan melihat ada metode transaksi apa saja pada kumpulan data ini yang ada pada fitur type, ternyata pada fitur type ada lima jenis metode transaksi, yaitu:

- Payment
- Transfer
- Cash Out
- Debit
- Cash in

Sebaran data fitur _type_ metode transaksi _cash_out_ menjadi yang tertinggi sebanyak 35% dan _debit_ menjadi yang terkecil yakni 0.7%.

gambar 2. sebaran data pada fitur _type_

![image](https://github.com/roamercodes/online-payment-fraud-detection/assets/22432578/38b2d545-66f0-4093-93a0-d1330b9a2521)

Pada fitur isFraud berisi _boolean_ label target yakni 0 dan 1, ada 6354407 untuk label 0 dan 8213 untuk label 1 yang berarti ada 8213 ditandai sebagai transaksi penipuan. Jika dilihat dari total data maka untuk transaksi yang ditandai penipuan hanya 0.13%

Kemudian pada kolom _isFraud_ transaksi penipuan hanya terjadi di 2 metode transaksi, yakni _cash_out_ dan _transfer_

Tabel 3. transaksi penipuan pada fitur _isFraud_ 

| type | 0 | 1 |
| ---- | - | - |
| CASH_IN | 1399284 | 0 |
| CASH_OUT | 2233384 | 4116 |
| DEBIT | 41432 | 0 |
| PAYMENT | 2151495 | 0 |
| TRANSFER | 528812 | 4097 |

Pada kolom _isFlaggedFraud_ ada 16 transaksi yang ditandai sebagai penipuan melibatkan transfer lebih dari 200.000 unit dalam mata uang tertentu. Karena terlalu sedikit, maka fitur tersebut tidak akan digunakan.

Tabel 4. jumlah transaksi penipuan pada fitur _isFlaggedFraud_

| type | 0 | 1 |
| ---- | - | - |
| CASH_IN | 1399284 | 0 |
| CASH_OUT | 2233384 | 0 |
| DEBIT | 41432 | 0 |
| PAYMENT | 2151495 | 0 |
| TRANSFER | 528812 | 16 |

### Multivariate Analysis

- Korelasi antar fitur numerik

gambar 3. matriks korelasi antar fitur numerik

![image](https://github.com/roamercodes/online-payment-fraud-detection/assets/22432578/1fbbe7b9-d309-4603-b6eb-e6f0659884e1)

  - _newbalanceOrig_ dan _oldbalanceOrg_ memiliki korelasi yang tinggi.
  -  _newbalanceDest_ dan _oldbalanceDest_ juga memiliki korelasi tinggi.
  -  Selain itu, korelasi yang relatif tinggi juga ada antara _amount_ dan _newbalanceDest_ dan _amount_ dengan _oldbalanceDes_

## Data Preparation

Fitur pada kolom _type_ masih bertipe objek, agar dapat diolah oleh algoritma maka perlu dilakukan perubahan menjadi numerik atau biasa disebut _One Hot Encoding_. Hal pertama yang dilakukan untuk mengkonversi isi kolom fitur adalah membuat _list dictionary_ yang _key_-nya adalah isi kolom dari fitur _type_ dan _value_-nya adalah _numeric_ yang mewakili, kemudian menggunakan fungsi _`map`_ untuk mengkonversi seluruh data pada kolom _type_ sesuai dengan _key_ dan _value_-nya_.

Pembagian data untuk data latih dan data tes, data latih digunakan pada proses pembelajaran dalam membangun model sedangkan data tes digunakan pada proses evaluasi kinerja model. Pembagian proporsi data latih dan data tes didasari dengan metode pembagian data yaitu _cross validation_ dimana dapat menggunakan proporsi tertentu tergantung dari proporsi dataset yang dimiliki, umumnya adalah `7:3`, `8:2` dan `9:1`, karena data pada penelitian ini cukup memadai maka proporsi pembagian data yang dipilih adalah 7:3, jika telah mencapai hasil yang memuaskan yaitu _accuracy_ diatas 90% maka cukup menggunakan satu _k-fold_ saja. Dari total dataset 6362620 maka data latih mendapat 4453834 dan data tes mendapat 1908786. 

## Modeling
Model algoritma pada penelitian ini menggunakan 3 model algoritma, yaitu [Logistic Regression](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegressionCV.html), [Random Forest](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html), [XGBoost](https://xgboost.readthedocs.io/en/stable/).

- _Logistic Regression_
  Regresi logistik adalah teknik analisis data yang menggunakan matematika untuk menemukan hubungan antara dua faktor data. Kemudian menggunakan hubungan ini untuk memprediksi nilai dari salah satu faktor tersebut berdasarkan faktor yang lain. Prediksi biasanya memiliki jumlah hasil yang terbatas, seperti ya atau tidak. _Logistic Regression_ menggunakan probabilitas untuk memprediksi klasifikasi data kategorikal. Nilai input dapat digabungkan secara linier menggunakan fungsi sigmoid atau logistik dan nilai koefisien untuk memprediksi hasil. Estimasi kemungkinan maksimum dianggap menggunakan fungsi sigmoid untuk mengasumsikan data yang paling mungkin dan probabilitas diberikan antara 0 sampai 1 mengatakan apakah suatu peristiwa akan terjadi atau tidak [5].

Parameter yang digunakan pada mmodel ini adalah:

- `cv` = `5` : fungsi untuk melakukan _k-fold cross validation_.
- `max_iter` = `500` : jumlah maksimum iterasi algoritma.
- `random_state` = `0` : Fungsi untuk mengkontrol _seed_ acak yang diberikan pada setiap pada setiap iterasi.
  
  - Kelebihan
    
    Regression models logistik tidak hanya model klasifikasi, tetapi juga memberikan probabilitas. Ini adalah keuntungan besar dibandingkan model yang hanya dapat memberikan klasifikasi akhir. Mengetahui bahwa sebuah _instance_ memiliki probabilitas 99% untuk suatu kelas dibandingkan dengan 51% membuat perbedaan besar.
  - Kelemahan
    
    Regression models logistik memiliki kelemahan interpretasinya lebih sulit karena interpretasi bobotnya bersifat perkalian dan tidak aditif. Logistic regression dapat mengalami pemisahan lengkap. Jika ada fitur yang akan memisahkan kedua kelas secara sempurna, regression models logistik tidak dapat lagi dilatih. Ini karena bobot untuk fitur itu tidak akan konvergen, karena bobot optimalnya tidak terbatas. Ini benar-benar agak disayangkan, karena fitur seperti itu sangat berguna. Tetapi Anda tidak memerlukan _machine learning_ jika Anda memiliki aturan sederhana yang memisahkan kedua kelas. Masalah pemisahan lengkap dapat diselesaikan dengan memperkenalkan _penalty_ bobot atau mendefinisikan distribusi probabilitas bobot sebelumnya.
    
- _Random Forest_

  _Random Forest_ membuat prediksi kategori dengan beberapa nilai yang mungkin dan dapat dikalibrasi untuk probabilitas _output_. Satu hal yang perlu diwaspadai adalah _overfitting_. _Random Forest_ rawan terjadi _overfitting_, terutama ketika bekerja dengan dataset yang relatif kecil. Perlu di curigai jika model data dapat membuat prediksi yang "terlalu bagus" pada set uji menggunakan _Random Forest_. Salah satu cara _overfitting_ adalah menggunakan fitur yang benar-benar relevan dalam model data yang digunakan.

Parameter yang digunakan pada model ini:

- `n_estimators` = `20`: Jumlah maksimum estimator di mana _boosting_ dihentikan.
- `random_state` = `0` : Fungsi untuk mengontrol _seed_ acak yang diberikan pada setiap pada setiap iterasi.
- `max_depth`    = `6` : Jumlah kedalaman maksimum setiap _tree_.
  
  - Kelebihan
  
    - Menghasilkan eror yang lebih rendah.
    - Memberikan hasil yang bagus dalam klasifikasi.
    - Dapat mengatasi data training dalam jumlah sangat besar secara efisien.
    - Metode yang efektif untuk mengestimasi hilangnya data.
    - Dapat memperkiraan variabel apa yang penting dalam klasifikasi.
    - Menyediakan metode eksperimental untuk mendeteksi interaksi variabel.
  
  - Kekurangan 

    - Waktu pemrosesan yang lama karena menggunakan data yang banyak dan membangun model _tree_ yang banyak pula untuk membentuk _random trees_ karena menggunakan _single processor_.
    - Interpretasi yang sulit dan membutuhkan mode penyetelan yang tepat untuk data.
    - ketika digunakan untuk regresi, mereka tidak dapat memprediksi di luar kisaran dalam data percobaan, hal ini di mungkinkan data terlalu cocok dengan kumpulan data pengganggu (noisy).
    
- _XGBoost_

  Algoritma _Gradient Boosting_ bekerja dengan menggabungkan beberapa model yang lemah menjadi sebuah model yang lebih kuat. Algoritma ini menggunakan pendekatan iteratif, di mana setiap iterasi bertujuan untuk meningkatkan model sebelumnya dengan menambahkan model baru. Proses ini dilakukan secara berulang-ulang hingga model yang dihasilkan memenuhi kriteria tertentu, seperti nilai loss function yang cukup kecil. Pada model _XGBoost_ tidak melakukan _tuning parameter_ hanya menginputkan `x_train` dan `y_train` saja.
  
  - Kelebihan
  
    - Akurasi yang tinggi: _Gradient Boosting_ sering menghasilkan model yang akurat dan kuat, terutama ketika digunakan pada data yang kompleks dan tidak terstruktur.
    - Tidak memerlukan persyaratan data yang ketat: Algoritma ini dapat digunakan pada berbagai jenis data tanpa memerlukan asumsi yang ketat, seperti asumsi tentang distribusi data atau homoskedastisitas.
    - Kecepatan komputasi yang cepat: Beberapa implementasi dari _Gradient Boosting_, seperti _XGBoost_ dan _LightGBM_, dapat digunakan untuk mempercepat waktu komputasi dengan teknik-teknik seperti _parallel computing_ dan _caching_.

  - Kekurangan
  
    - Memerlukan tuning yang cermat: Algoritma ini memerlukan tuning parameter yang cermat untuk mendapatkan model yang optimal. Hal ini dapat memakan waktu dan mengharuskan penggunaan _cross-validation_ dan teknik _tuning parameter_ lainnya.
    - Mudah _overfitting_: _Gradient Boosting_ dapat cenderung _overfit_ pada data latih jika tidak dilakukan pengaturan parameter yang baik. _Overfitting_ terjadi ketika model terlalu kompleks dan terlalu menyesuaikan dengan data latih, sehingga tidak dapat melakukan generalisasi dengan baik pada data yang belum pernah dilihat sebelumnya.
    - Memerlukan data yang besar: _Gradient Boosting_ memerlukan jumlah data yang besar untuk memperoleh model yang akurat dan stabil. Jika jumlah data terlalu sedikit, algoritma ini dapat menjadi tidak stabil dan menghasilkan model yang tidak akurat.

Model terbaik didapat pada XGBoost, dengan menggunakan model ini mampu mendapatkan akurasi data latih maupun data tes tertinggi daripada model lainnya, data yang digunakan juga sangat besar hal ini dapat menutupi kekurangan pada model _XGBoost_.

## Evaluation

Evaluasi berguna untuk mengukur seberapa baik model ketika pengujian, pada penelitian ini untuk mengevaluasi performa model maka akan menggunakan metrik evaluasi yaitu _confussion matriks_ **akurasi, precision, recall, dan F1 score**. Dari sebuah matriks konfusi kita bisa mendapatkan nilai-nilai seperti _true positive (TP)_, _false positive (FP)_, _true negative (TN)_, dan f_alse negative (FN)_. Setiap nilai yang disebutkan dapat digunakan untuk mendapatkan  _precision, F1, recall & accuracy_. Persamaan di bawah ini menunjukan fungsi dari keempat istilah tersebut :

- Akurasi adalah hasil prediksi yang benar dari keseluruhan data uji.

| $$Accuracy = \frac {TP + TN} { TP + FP + FN + TN }$$ |
| ---------------------------------------------------- |

- Presisi adalah prediksi rasio TP dibanding keseluruhan prediksi positif.

| $$Precision = \frac {TP} { TP + FP }$$ |
| -------------------------------------- |

- Recall adalah prediksi rasio TP dibanding keseluruhan data yang benar.

| $$Recall = \frac {TP} {TP + FN }$$ |
| ---------------------------------- |
  
- F1-score adalah perbandingan sebuah rata-rata presisi dan recall.

| $$F1 = \frac {2   x   Recall   x   Precision} { Recall + Precision }$$ |
| -------------------------------------------------------------------- |

Berikut hasil akurasi _training_ dan _testing_ pada masing-masing model yang digunakan:

Tabel 5. hasil akurasi data latih dan data tes dari 3 algoritma

| models | train | test |
| ------ | :---: | ---: |
| random forest | 99.93% | 99.93% |
| logistic regression | 99.82% | 99.82% |
| xgboost | 99.98% | 99.98% |
 
   
Berikut hasil evaluasi pada penelitian ini yaitu pada model _Random Forest_ :

Tabel 6. hasil _precision_, _f1-score_ dan _support_ model _random forest_.

| class | precision | recall | f1-score | support |
| ----- | --------- | ------ | -------- | ------- |
|   0   |   1.00    |  1.00  |   1.00   | 1906318 |
|   1   |   1.00    |  0.47  |   0.64   |  2468   |

Pada tabel 6. hasil _Precision recall_ dan _F1 Score_ untuk kelas/label 0 (bukan transaksi penipuan) sangat baik, dimana tingkat presisi, keberhasilan model menemukan kembali sebuah informasi pada label 0 semua mendapat 100%.
Berbeda pada label 1 (transaksi penipuan) akurasi antara data yang diminta dengan hasil prediksi yang diberikan oleh model atau _precision_ mendapat nilai yang baik, sedangkan keberhasilan model menemukan kembali sebuah informasi atau _recall_ cukup buruk yakni 47% dan perbandingan rata-rata _precision_ dan _recall_ yang dibobotkan atau _F1 Score_ mendapatkan nilai 64%. Maka metrik yang dapat dijadikan acuan pada model ini adalah _accuracy_ pada performa algoritma.

Berikut hasil evaluasi pada penelitian ini yaitu pada model _Logistic Regression_ :

Tabel 7. hasil _precision_, _f1-score_ dan _support_ model _logistic regression_.

| class | presision | recall | f1-score | support |
| ----- | --------- | ------ | -------- | ------- |
|   0   |   1.00    |  1.00  |   1.00   | 1906318 |
|   1   |   0.34    |  0.41  |   0.38   |  2468   |

Pada tabel 7. hasil _Precision recall_ dan _F1 Score_ untuk kelas/label 0 (bukan transaksi penipuan) sangat baik, dimana tingkat presisi, keberhasilan model menemukan kembali sebuah informasi pada label 0 semua mendapat 100%.
Sedangkan pada label 1 (transaksi penipuan) akurasi antara data yang diminta dengan hasil prediksi yang diberikan oleh model atau _precision_ mmendapat nilai yang buruk yakni 34%, sedangkan keberhasilan model menemukan kembali sebuah informasi atau _recall_ cukup buruk yakni 41% dan perbandingan rata-rata _precision_ dan _recall_ yang dibobotkan atau _F1 Score_ juga cukup buruk yakni mendapatkan nilai 38%. Maka metrik yang dapat dijadikan acuan pada model ini adalah _accuracy_ pada performa algoritma.

Berikut hasil evaluasi pada penelitian ini yaitu pada model _XGBoost_ :

Tabel 8. hasil _precision_, _f1-score_ dan _support_ model _XGBoost_.

| class | presision | recall | f1-score | support |
| ----- | --------- | ------ | -------- | ------- |
|   0   |   1.00    |  1.00  |   1.00   | 1906318 |
|   1   |   0.97    |  0.87  |   0.92   |  2468   |

Pada tabel 7. dari model XGBoost inilah kedua label 0 dan 1 hasil _Precision recall_ dan _F1 Score_ mendapatkan nilai yang bagus, tidak hanya akurasi dari data latih maupun data uji. Pada kasus ini, _XGBoost_ menjadi model terbaik.

## Kesimpulan

Transaksi secara elektronik dimasa modern akan terus selalu meningkat dan berkembang, tidak dapat dipungkiri juga dari kemudahan bertransaksi tersebut akan dapat disalahgunakan. Pada penelitian ini terkait dengan memprediksi transaksi penipuan. Maka dari 3 model algoritma yaitu _Random Forest_, _Logistic Regresion_ dan _XGBoost_ berhasil mendapatkan hasil yang sesuai ekspetasi dengan akurasi diatas 99% dan dengan adanya pembelajaran mesin maka dapat membantu mendeteksi adanya transaksi penipuan. Diharapkan pada masa mendatang tingkat prediksi dapat mencakup jenis atau metode transaksi yang lebih luas lagi agar dapat meminimalisir tingkat kerugian pada pihak-pihak terkait.

## Daftar Pustaka

[1]	N. A. Rakhmawati, A. E. Permana, A. M. Reyhan, and H. Rafli, “ANALISA TRANSAKSI BELANJA ONLINE PADA MASA PANDEMI COVID-19,” J. Teknoinfo, vol. 15, no. 1, Art. no. 1, Jan. 2021, doi: 10.33365/jti.v15i1.868.

[2]	Faried Zamachsari and Niken Puspitasari, “Penerapan Deep Learning dalam Deteksi Penipuan Transaksi Keuangan Secara Elektronik | Jurnal RESTI (Rekayasa Sistem dan Teknologi Informasi),” Apr. 2021, Accessed: Jun. 21, 2023. [Online]. Available: http://jurnal.iaii.or.id/index.php/RESTI/article/view/2952

[3]	N. Rahmad, “Kajian Hukum terhadap Tindak Pidana Penipuan Secara Online,” J. Huk. Ekon. Syariah, vol. 3, no. 2, Art. no. 2, Dec. 2019, doi: 10.26618/j-hes.v3i2.2419.

[4]	I. Kurniawan, “Perkembangan Tindak Pidana Pencucian Uang (Money Laundering) Dan Dampaknya Terhadap Sektor Ekonomi Dan Bisnis,” J. Ilmu Huk., vol. 4, no. 1, Art. no. 1, Mar. 2013, doi: 10.30652/jih.v3i1.1037.

[5]	F. Handayani, “Komparasi Support Vector Machine, Logistic Regression Dan Artificial Neural Network Dalam Prediksi Penyakit Jantung,” JEPIN J. Edukasi Dan Penelit. Inform., vol. 7, no. 3, Art. no. 3, Dec. 2021, doi: 10.26418/jp.v7i3.48053.

[6]	G. H. Cahyono, “MENGENAL ELEKTRONIK BANKING,” Swara Patra Maj. Ilm. PPSDM Migas, vol. 5, no. 1, Art. no. 1, Dec. 2015, Accessed: Jun. 21, 2023. [Online]. Available: http://ejurnal.ppsdmmigas.esdm.go.id/sp/index.php/swarapatra/article/view/125

[7]	O. Raiter, “Applying Supervised Machine Learning Algorithms for Fraud Detection in Anti-Money Laundering”.

[8]	E. A. Lopez-Rojas and C. Barneaud, “Advantages of the PaySim Simulator for Improving Financial Fraud Controls,” in Intelligent Computing, K. Arai, R. Bhatia, and S. Kapoor, Eds., in Advances in Intelligent Systems and Computing, vol. 998. Cham: Springer International Publishing, 2019, pp. 727–736. doi: 10.1007/978-3-030-22868-2_51.
