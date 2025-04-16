# Laporan Proyek Machine Learning - Prediksi Gaji di Indonesia & Studi Kasus Jawa Timur
 
## A. Domain Proyek
 
Prediksi gaji menjadi aspek penting dalam perencanaan ekonomi, baik untuk individu, perusahaan, maupun pemerintah. Dengan memahami tren historis gaji, kita dapat mengantisipasi perubahan ekonomi, mengatur kebijakan upah minimum, dan membantu pengusaha dalam menetapkan standar gaji yang kompetitif.
 
**Mengapa masalah ini penting?**
- Membantu perencanaan tenaga kerja untuk bisnis dan industri.
- Mendukung kebijakan upah minimum dengan prediksi berbasis data.
- Memberikan wawasan tren gaji kepada pekerja dan pengusaha.
- Dapat diperluas ke skala regional untuk analisis spesifik per provinsi.
 
Selain memprediksi gaji secara nasional, laporan ini juga mencakup prediksi khusus untuk Jawa Timur sebagai contoh penerapan analisis berbasis wilayah.
 
---
 
## B. Business Understanding
 
### Problem Statements
1. Bagaimana tren kenaikan gaji di Indonesia dalam beberapa tahun terakhir?
2. Algoritma apa yang paling efektif untuk memprediksi gaji berdasarkan data historis?
3. Bagaimana prediksi gaji untuk 1, 2, dan 3 tahun ke depan?
4. Bagaimana perbandingan tren gaji nasional dengan provinsi tertentu, seperti Jawa Timur?
 
### Goals
1. Menghasilkan model prediksi gaji dengan error yang minimal.
2. Membandingkan performa ARIMA dan LSTM dalam forecasting gaji.
3. Menganalisis tren kenaikan gaji di Indonesia secara keseluruhan.
4. Menguji model dengan studi kasus di Jawa Timur untuk melihat perbedaan regional.
 
### Solution Statements
- Menggunakan **data gaji dari tahun 1997-2022** untuk membangun model prediksi.
- Menggunakan **ARIMA** (statistik) dan **LSTM** (deep learning) untuk perbandingan model.
- Melakukan **hyperparameter tuning** pada model LSTM agar lebih akurat.
- Menggunakan **RMSE, MAE, dan MSE** untuk mengevaluasi model.
- Membuat **prediksi 1, 2, dan 3 tahun ke depan** untuk skala nasional & Jawa Timur.
 
---
 
## C. Data Understanding
 
Dataset yang digunakan berisi informasi gaji di berbagai wilayah Indonesia dari tahun 1997 hingga 2022 dengan variabel berikut:
- **REGION**: Wilayah yang dicatat.
- **SALARY**: Jumlah gaji rata-rata.
- **YEAR**: Tahun pencatatan data.
 
   Dataset : [Sumber Dataset](https://www.kaggle.com/datasets/linkgish/indonesian-salary-by-region-19972022)
 
Jumlah data : **870 sampel** (lebih dari 500, sesuai kriteria submission).
 
**Exploratory Data Analysis (EDA):**
- ✔ Tren kenaikan gaji dari tahun ke tahun.
- ✔ Distribusi gaji di berbagai wilayah.
- ✔ Korelasi antara tahun dan rata-rata gaji.
 
![image](https://github.com/user-attachments/assets/692eee06-1b16-4fde-ac04-4ac70899c5dc)
 
Visualisasi diatas menunjukkan bahwa : Gaji nasional cenderung meningkat setiap tahun, tetapi dengan pola fluktuatif di beberapa tahun.
 
---
 
## D. Data Preparation
 
- **Cleaning Data**: Menghapus data yang hilang dan duplikasi.
*Alasan :* Memastikan data tidak mengandung noise yang mengganggu model.
- **Aggregasi Data**: Menghitung rata-rata gaji per tahun untuk analisis time series.
*Alasan :* Agar tren lebih terlihat jelas pada skala nasional & regional.
- **Scaling Data**: Normalisasi gaji agar lebih stabil saat diproses oleh model LSTM.
*Alasan :* LSTM bekerja lebih baik dengan data ter-normalisasi.
- **Splitting Data**: Membagi data menjadi **training (80%)** dan **testing (20%)**.
*Alasan :* Memastikan model diuji dengan data yang belum pernah dilihat sebelumnya.
- **Time Series Transformation**: Mengubah data agar sesuai dengan format sequence untuk LSTM.
*Alasan :* Memungkinkan model menangkap pola perubahan gaji.
 
---
 
## E. Modeling
 
Model yang digunakan:
1. **ARIMA (AutoRegressive Integrated Moving Average)** untuk model statistik.
2. **LSTM (Long Short-Term Memory)** untuk model berbasis deep learning.
 
**Parameter yang digunakan:**
- ARIMA: Parameter (p, d, q) ditentukan berdasarkan analisis ACF & PACF.
- LSTM: 2 Layer LSTM, 100 neuron per layer, Dropout 20%, Optimizer Adam, 100 epoch.
 
**Kelebihan & Kekurangan**
- **ARIMA** bekerja baik dengan dataset kecil tetapi kurang optimal untuk pola yang kompleks.
- **LSTM** lebih unggul dalam menangkap pola jangka panjang tetapi membutuhkan data dalam jumlah besar dan lebih banyak komputasi.
 
**Improvement Model**
- Hyperparameter tuning untuk meningkatkan performa model.
- Cross-validation untuk menghindari overfitting.

**Cara Kerja Model**
1. ARIMA (AutoRegressive Integrated Moving Average), ARIMA adalah model statistik untuk analisis deret waktu yang menggabungkan tiga komponen utama:
- AutoRegressive (AR): Model menggunakan nilai masa lalu untuk memprediksi nilai saat ini.
- Integrated (I): Menggunakan differencing (pengurangan antar waktu) untuk membuat data menjadi stasioner.
- Moving Average (MA): Menggunakan error dari prediksi sebelumnya sebagai bagian dari model saat ini.

Prosesnya dimulai dengan memastikan data stasioner (melalui differencing), lalu menganalisis ACF dan PACF untuk menentukan parameter p, d, dan q, dan akhirnya membangun model ARIMA yang memprediksi nilai masa depan berdasarkan pola historis.

2. LSTM (Long Short-Term Memory), LSTM adalah tipe dari Recurrent Neural Network (RNN) yang dirancang untuk mengatasi masalah long-term dependency pada data sekuensial, seperti time series. LSTM menggunakan cell state dan gate (input, forget, dan output gate) untuk mengatur aliran informasi dalam jaringan.

Model LSTM membaca data urutan (misal gaji per tahun) dan belajar mengenali pola yang muncul dalam urutan tersebut. Karena LSTM mampu mengingat informasi penting dari masa lalu dalam jangka panjang, model ini cocok untuk memprediksi tren jangka panjang seperti gaji. Data gaji distandarisasi dan diubah ke bentuk sekuens (misalnya sliding window) agar bisa diproses oleh LSTM layer.
 
Model terbaik dipilih berdasarkan nilai RMSE dan MAE yang paling rendah.
 
---
 
## F. Evaluation
 
Metrik evaluasi yang digunakan:
1. **RMSE (Root Mean Squared Error)** - mengukur seberapa jauh prediksi dari nilai aktual.
   
   ![Screenshot 2025-03-14 163726](https://github.com/user-attachments/assets/98d13f6b-e51d-4dae-bb85-488a3cb3ed78)

 
3. **MAE (Mean Absolute Error)** - mengukur rata-rata error absolut dari prediksi.
 
   ![Screenshot 2025-03-14 163807](https://github.com/user-attachments/assets/e2232115-9b56-4a02-a61c-5479c6956619)

   
4. **MSE (Mean Squared Error)** – Mengukur error dengan memberi bobot lebih besar pada kesalahan yang lebih besar.
 
   ![Screenshot 2025-03-14 163856](https://github.com/user-attachments/assets/06b0d0a6-7490-44e4-9902-8540279ea171)

 
**Hasil Evaluasi Nasional**

ARIMA:
1. RMSE: Rp 2.69 jt
2. MAE : Rp 2.69 jt
3. MSE : Rp 7,210.08 M

LSTM:
1. RMSE: Rp 1.42 jt
2. MAE : Rp 1.42 jt
3. MSE : Rp 2,018.51 M

Insight yang diperoleh : 
- ARIMA memiliki nilai RMSE dan MAE sekitar Rp 2.69 juta, yang berarti rata-rata deviasi prediksi terhadap data aktual cukup besar.
- LSTM menunjukkan performa lebih baik dengan RMSE dan MAE sebesar Rp 1.42 juta, atau sekitar 47% lebih kecil dibanding ARIMA.
- Selisih MSE yang cukup signifikan (Rp 7,210.08 M vs Rp 2,018.51 M) menunjukkan bahwa LSTM jauh lebih stabil dan efektif dalam mereduksi error besar dalam prediksi.
- Artinya, untuk skala nasional, LSTM lebih andal untuk forecasting tren gaji, terutama saat menghadapi pola gaji yang fluktuatif di beberapa tahun terakhir.

Prediksi Gaji Nasional
- 2023: Rp 4.60 jt
- 2024: Rp 5.40 jt
- 2025: Rp 6.82 jt

Prediksi Gaji Jawa Timur
- 2023: Rp 3.00 jt
- 2024: Rp 3.53 jt
- 2025: Rp 4.44 jt
 
**Kesimpulan:**
- Model LSTM menghasilkan RMSE, MAE, dan MSE lebih rendah dibandingkan ARIMA, menunjukkan bahwa model deep learning lebih baik dalam menangkap pola tren gaji.
- LSTM unggul untuk prediksi baik nasional maupun regional (Jawa Timur).
- Prediksi gaji menunjukkan tren kenaikan yang signifikan baik secara nasional maupun di Jawa Timur dalam 3 tahun ke depan.
 
---
