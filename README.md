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

  - _newbalanceOrig_ dan _oldbalanceOrg_ meliki korelasi yang tinggi.
  -  _newbalanceDest_ dan _oldbalanceDest_ juga memiliki korelasi tinggi.
  -  Selain itu, korelasi yang relatif tinggi juga ada antara _amount_ dan _newbalanceDest_ dan _amount_ dengan _oldbalanceDes_

## Data Preparation

![image](https://github.com/roamercodes/online-payment-fraud-detection/assets/22432578/00dda550-c83c-4b38-9549-28680ccd4088)

Seperti pada gambar diatas, fitur pada kolom _type_ masih bertipe objek, agar dapat diolah oleh algorima maka perlu dilakukan perubahan menjadi numerik atau biasa disebut [One Hot Encoding](https://ilmudatapy.com/one-hot-encoding-di-python/).

Kemudian melakukan pembagian data untuk data latih dan data tes. Data latih digunakan pada proses pembelajaran dalam membangun model sedangkan data tes digunakan pada proses evaluasi kinerja model. Karena data cukup banyak maka pada proyek ini dilakukan pembagian sebanyak 70% untuk data latih dan 30% untuk data tes, jadi dari total dataset 6362620 maka data latih mendapat 4453834 dan data tes mendapat 1908786.

## Modeling
Model algoritma pada penelitian ini menggunakan 3 model algoritma, yaitu [Logistic Regression](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html) [Random Forest](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html) [XGBoost](https://xgboost.readthedocs.io/en/stable/).

- Logistic Regression
  Regresi logistik adalah teknik analisis data yang menggunakan matematika untuk menemukan hubungan antara dua faktor data. Kemudian menggunakan hubungan ini untuk memprediksi nilai dari salah satu faktor tersebut berdasarkan faktor yang lain. Prediksi biasanya memiliki jumlah hasil yang terbatas, seperti ya atau tidak. Logistic Regression menggunakan probabilitas untuk memprediksi klasifikasi data kategorikal. Nilai input dapat digabungkan secara linier menggunakan fungsi sigmoid atau logistik dan nilai koefisien untuk memprediksi hasil. Estimasi kemungkinan maksimum dianggap menggunakan fungsi sigmoid untuk mengasumsikan data yang paling mungkin dan probabilitas diberikan antara 0 sampai 1 mengatakan apakah suatu peristiwa akan terjadi atau tidak [Komparasi Support Vector Machine, Logistic Regression Dan Artificial Neural Network dalam Prediksi Penyakit Jantung](https://jurnal.untan.ac.id/index.php/jepin/article/view/48053/75676591338). 
  
  - Kelebihan
    
    Regression models logistik tidak hanya model klasifikasi, tetapi juga memberikan probabilitas. Ini adalah keuntungan besar dibandingkan model yang hanya dapat memberikan klasifikasi akhir. Mengetahui bahwa sebuah instance memiliki probabilitas 99% untuk suatu kelas dibandingkan dengan 51% membuat perbedaan besar. [Logistic Regression](https://interpretable-ml.keamanansiber.id/logistic.html)
  - Kelemahan
    
    Regression models logistik memiliki kelemahan interpretasinya lebih sulit karena interpretasi bobotnya bersifat perkalian dan tidak aditif. Logistic regression dapat mengalami pemisahan lengkap. Jika ada fitur yang akan memisahkan kedua kelas secara sempurna, regression models logistik tidak dapat lagi dilatih. Ini karena bobot untuk fitur itu tidak akan konvergen, karena bobot optimalnya tidak terbatas. Ini benar-benar agak disayangkan, karena fitur seperti itu sangat berguna. Tetapi Anda tidak memerlukan machine learning jika Anda memiliki aturan sederhana yang memisahkan kedua kelas. Masalah pemisahan lengkap dapat diselesaikan dengan memperkenalkan penalty bobot atau mendefinisikan distribusi probabilitas bobot sebelumnya. [Logistic Regression](https://interpretable-ml.keamanansiber.id/logistic.html)
    
- Random Forest

  Random Forest membuat prediksi kategori dengan beberapa nilai yang mungkin dan dapat dikalibrasi untuk probabilitas output. Satu hal yang perlu diwaspadai adalah overfitting. Random Forest rawan terjadi overfitting, terutama ketika bekerja dengan dataset yang relatif kecil. Perlu di curigai jika model data dapat membuat prediksi yang "terlalu bagus" pada set uji menggunakan Random Forest. Salah satu cara overfitting adalah menggunakan fitur yang benar-benar relevan dalam model data yang digunakan. [Algoritma Random Forest](https://learningbox.coffeecup.com/05_2_randomforest.html)
  
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

  Algoritma Gradient Boosting bekerja dengan menggabungkan beberapa model yang lemah menjadi sebuah model yang lebih kuat. Algoritma ini menggunakan pendekatan iteratif, di mana setiap iterasi bertujuan untuk meningkatkan model sebelumnya dengan menambahkan model baru. Proses ini dilakukan secara berulang-ulang hingga model yang dihasilkan memenuhi kriteria tertentu, seperti nilai loss function yang cukup kecil. 
  
  - Kelebihan
  
    - Akurasi yang tinggi: Gradient Boosting sering menghasilkan model yang akurat dan kuat, terutama ketika digunakan pada data yang kompleks dan tidak terstruktur.
    - Tidak memerlukan persyaratan data yang ketat: Algoritma ini dapat digunakan pada berbagai jenis data tanpa memerlukan asumsi yang ketat, seperti asumsi tentang distribusi data atau homoskedastisitas.
    - Kecepatan komputasi yang cepat: Beberapa implementasi dari Gradient Boosting, seperti XGBoost dan LightGBM, dapat digunakan untuk mempercepat waktu komputasi dengan teknik-teknik seperti parallel computing dan caching.

  - Kekurangan
  
    - Memerlukan tuning yang cermat: Algoritma ini memerlukan tuning parameter yang cermat untuk mendapatkan model yang optimal. Hal ini dapat memakan waktu dan mengharuskan penggunaan cross-validation dan teknik tuning parameter lainnya.
    - Mudah overfitting: Gradient Boosting dapat cenderung overfit pada data training jika tidak dilakukan pengaturan parameter yang baik. Overfitting terjadi ketika model terlalu kompleks dan terlalu menyesuaikan dengan data training, sehingga tidak dapat melakukan generalisasi dengan baik pada data yang belum pernah dilihat sebelumnya.
    - Memerlukan data yang besar: Gradient Boosting memerlukan jumlah data yang besar untuk memperoleh model yang akurat dan stabil. Jika jumlah data terlalu sedikit, algoritma ini dapat menjadi tidak stabil dan menghasilkan model yang tidak akurat.

Model terbaik didapat pada XGBoost, dengan menggunakan model ini mampu mendapatkan akurasi data latih maupun data tes tertinggi daripada model lainnya, data yang digunakan juga sangat besar hal ini dapat menutupi kekurangan pada model XGBoost.

## Evaluation

Evaluasi berguna untuk mengukur seberapa baik model ketika pengujian, pada penelitian ini untuk mengevaluasi performa model maka akan mengguanakan metrik evaluasi yaitu _confussion matriks_ **akurasi, precision, recall, dan F1 score**. Dari sebuah matriks konfusi kita bisa mendapatkan nilai-nilai seperti true positive (TP), false positive (FP), true negative (TN), dan false negative (FN). Setiap nilai yang disebutkan dapat digunakan untuk mendapatkan  presisi, F1, recall dan akurasi [Understanding Confusion Matrix](https://towardsdatascience.com/understanding-confusion-matrix-a9ad42dcfd62). Persamaan di bawah ini menunjukan fungsi dari keempat istilah tersebut :

- Akurasi adalah hasil prediksi yang benar dari keseluruhan data uji.

  ![image](https://github.com/roamercodes/online-payment-fraud-detection/assets/22432578/d638fec0-4c47-4b04-b243-2ebd2afdb117)

- Presisi adalah prediksi rasio TP dibanding keseluruhan prediksi positif. 

  ![image](https://github.com/roamercodes/online-payment-fraud-detection/assets/22432578/255335b4-ca63-42c3-bf25-4287b10596f7)

- Recall adalah prediksi rasio TP dibanding keseluruhan data yang benar.

  ![image](https://github.com/roamercodes/online-payment-fraud-detection/assets/22432578/cb0f77cc-6621-49be-8b43-49b3d4deb8a7)

- F1-score adalah perbandingan sebuah rata-rata presisi dan recall.

  ![image](https://github.com/roamercodes/online-payment-fraud-detection/assets/22432578/e986f4f8-1824-4652-a1b9-5c4adeeec503)

Berikut hasil akurasi _training_ dan _testing_ pada masing-masing model yang digunakan:

| models | train | test |
| ------ | :---: | ---: |
| random forest | 99.93% | 99.93% |
| logistic regression | 99.82% | 99.82% |
| xgboost | 99.98% | 99.98% |
 
   
Berikut hasil evaluasi pada penelitian ini yaitu pada model _Random Forest_ :

| class | presision | recall | f1-score | support |
| ----- | --------- | ------ | -------- | ------- |
|   0   |   1.00    |  1.00  |   1.00   | 1906318 |
|   1   |   1.00    |  0.47  |   0.64   |  2468   |

  
Berikut hasil evaluasi pada penelitian ini yaitu pada model _Logistic Regression_ :

| class | presision | recall | f1-score | support |
| ----- | --------- | ------ | -------- | ------- |
|   0   |   1.00    |  1.00  |   1.00   | 1906318 |
|   1   |   0.34    |  0.41  |   0.38   |  2468   |

  
Berikut hasil evaluasi pada penelitian ini yaitu pada model _XGBoost_ :

| class | presision | recall | f1-score | support |
| ----- | --------- | ------ | -------- | ------- |
|   0   |   1.00    |  1.00  |   1.00   | 1906318 |
|   1   |   0.97    |  0.87  |   0.92   |  2468   |

