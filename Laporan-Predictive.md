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
 
![image](https://github.com/user-attachments/assets/6d0b9b32-6ed5-4498-b599-1ed5928f2561)
 
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
 
Model terbaik dipilih berdasarkan nilai RMSE dan MAE yang paling rendah.
 
---
 
## F. Evaluation
 
Metrik evaluasi yang digunakan:
1. **RMSE (Root Mean Squared Error)** - mengukur seberapa jauh prediksi dari nilai aktual.
   
   ![image](https://github.com/user-attachments/assets/948cc8f0-0cf7-48b1-9c3f-c3ac993f2825)
 
3. **MAE (Mean Absolute Error)** - mengukur rata-rata error absolut dari prediksi.
 
   ![image](https://github.com/user-attachments/assets/d5a3871a-4899-4085-91cd-04f346a9440d)
 
   
4. **MSE (Mean Squared Error)** – Mengukur error dengan memberi bobot lebih besar pada kesalahan yang lebih besar.
 
   ![image](https://github.com/user-attachments/assets/17429587-bf89-452d-b191-e42a098b758e)
   
 
**Hasil Evaluasi Nasional**
1. ARIMA RMSE: 2.68 juta
2. LSTM RMSE (denormalized): 1.04 juta
 
**Hasil Evaluasi Jawa Timur**
1. ARIMA RMSE (Jawa Timur): 2.3 juta
2. LSTM RMSE (Jawa Timur, denormalized): 980 ribu
 
- Model **LSTM** menghasilkan RMSE lebih rendah dibandingkan **ARIMA**, menunjukkan bahwa model deep learning lebih baik dalam menangkap pola tren gaji.
- MAE dari LSTM juga lebih rendah, menunjukkan prediksi yang lebih stabil dibandingkan ARIMA.
 
**Kesimpulan:**
- LSTM lebih unggul dibandingkan ARIMA dalam menangkap pola tren gaji, baik secara nasional maupun regional.
- RMSE dan MAE LSTM lebih kecil dibanding ARIMA, menunjukkan prediksi yang lebih akurat dan stabil.
- MSE LSTM lebih kecil dibanding ARIMA, menunjukkan bahwa model deep learning mampu mengurangi kesalahan besar lebih baik dibanding model statistik.
 
---
