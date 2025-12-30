# Tugas Analisis Statistik: Deskriptif, Korelasi, dan Regresi

## 1. Informasi Penyusun

- **Nama:** `[LEONITA SYAKIRA AL KARIIRI PUTERI KAMULYANING JAGAD]`
- **NIM:** `[2515101081]`
- **Program Studi:** `[ILMU KOMPUTER]`
- **Mata Kuliah:** Statistika dan Probabilitas

---

## 2. Deskripsi Proyek

Dataset yang digunakan dalam analisis ini merupakan data startup yang berisi informasi mengenai kondisi bisnis dan perilaku pelanggan dari sejumlah startup. Data ini mencakup enam variabel utama, yaitu Nama_Startup, Kategori_Layanan, Pendapatan_Tahunan_Miliar_IDR, Biaya_Akuisisi_Pelanggan_Juta_IDR, Nilai_Pelanggan_Juta_IDR, dan Tingkat_Churn_Persen. Beberapa variabel dalam dataset berbentuk numerik dan digunakan untuk menggambarkan kinerja finansial serta hubungan dengan pelanggan, seperti pendapatan tahunan, biaya akuisisi pelanggan, nilai pelanggan, dan tingkat churn. Sementara itu, variabel nama startup dan kategori layanan digunakan sebagai informasi pendukung untuk membedakan karakteristik masing-masing startup. Tujuan dari analisis ini sendiri adalah untuk memahami gambaran umum kondisi startup melalui statistik deskriptif, dan melihat hubungan antar variable dalam dataset.

---

## 3. Struktur Proyek

Proyek ini diorganisir ke dalam beberapa folder:
- `/data`: Berisi dataset mentah yang digunakan untuk analisis.
- `/scripts`: Berisi semua skrip R yang digunakan dalam analisis, diurutkan berdasarkan alur kerja.
- `/results`: Berisi output dari analisis, seperti plot, gambar, atau tabel ringkasan.

---

## 4. Cara Menjalankan Analisis

Untuk mereproduksi hasil analisis ini, ikuti langkah-langkah berikut:
1. Pastikan Anda memiliki R dan RStudio terinstal.
2. Buka proyek R ini di RStudio.
3. Instal paket yang diperlukan dengan menjalankan perintah berikut di konsol R:
   ```R
   # install.packages(c("tidyverse", "corrplot", "knitr"))
   ```
4. Jalankan skrip di dalam folder `/scripts` secara berurutan, mulai dari `01_data_preparation.R` hingga `05_analisis_regresi.R`.

---

## 5. Hasil dan Interpretasi

Di bagian ini, mahasiswa diharapkan untuk menyajikan dan menginterpretasikan hasil dari setiap tahap analisis.

### 5.1. Statistik Deskriptif
- **Ukuran Pemusatan (Mean, Median, Modus):**
  - *Mean: 31.88, Median: 31.30, Modus: 1.87*
  - *Interpretasi: Nilai mean pendapatan tahunan startup sebesar 31.88 miliar rupiah, sedangkan median sebesar 31.30 miliar rupiah, yang menunjukkan bahwa secara umum pendapatan startup berada di kisaran tersebut. Namun, nilai modus yang jauh lebih kecil, yaitu 1.87 miliar rupiah, menunjukkan bahwa pendapatan yang paling sering muncul berasal dari startup dengan skala yang lebih kecil. Perbedaan ini mengindikasikan adanya variasi pendapatan antar startup, di mana beberapa startup dengan pendapatan tinggi turut menaikkan nilai rata-rata.*

- **Ukuran Sebaran (Standar Deviasi, Range, Kuartil):**
  - *Standar Deviasi: 19.79, Range: 1 - 66.89, Q1: 14.31, Q3: 49.04*
  - *Interpretasi: Berdasarkan nilai minimum dan maksimum, pendapatan tahunan startup berada pada rentang yang cukup lebar, yaitu dari 1.00 hingga 66.89 miliar rupiah, yang menunjukkan adanya perbedaan skala pendapatan yang besar antar startup. Nilai kuartil pertama (Q1) sebesar 14.31 miliar rupiah dan kuartil ketiga (Q3) sebesar 49.04 miliar rupiah menunjukkan bahwa 50% data berada di antara rentang tersebut, menandakan sebaran data yang cukup luas. Selain itu, selisih antara nilai minimum, kuartil, dan maksimum menunjukkan bahwa data tidak terkonsentrasi pada satu nilai tertentu, melainkan tersebar dengan variasi yang cukup tinggi.*

- **Visualisasi (Histogram/Boxplot):**
  - *<a href="#"><img src="results/histogram_Pendapatan_Tahunan_Miliar_IDR.png" /></a>*
  - *Interpretasi: Berdasarkan histogram pendapatan tahunan startup, terlihat bahwa data tersebar cukup merata di sepanjang rentang nilai, dengan frekuensi yang relatif seimbang dari pendapatan rendah hingga tinggi. Garis putus-putus merah yang menunjukkan nilai mean berada di sekitar 31,88 miliar rupiah, yang posisinya berada di tengah distribusi, menandakan bahwa tidak terdapat kemencengan (skewness) yang ekstrem ke kiri maupun ke kanan. Sebaran data yang lebar menunjukkan bahwa startup dalam dataset ini memiliki tingkat pendapatan yang sangat bervariasi, mulai dari startup berskala kecil hingga besar. Bentuk distribusi ini mengindikasikan bahwa tidak ada satu kelompok pendapatan tertentu yang mendominasi secara kuat, sehingga dataset mencerminkan kondisi startup yang cukup beragam dari sisi performa pendapatan.*


### 5.2. Uji Normalitas
- **Hasil Uji Shapiro-Wilk:**
  - *Nilai p-value = 1.497e-14*
  - *Interpretasi:Karena nilai p-value lebih kecil dari tingkat signifikansi 0,05, maka data tidak terdistribusi normal. Implikasinya, analisis lanjutan yang mengasumsikan distribusi normal (seperti uji parametrik tertentu) sebaiknya dilakukan dengan hati-hati. Untuk analisis hubungan antar variabel, metode non-parametrik atau pendekatan yang tidak bergantung pada asumsi normalitas dapat dipertimbangkan agar hasil analisis lebih valid.*

- **Plot Q-Q:**
  - *<a href="#"><img src="results/qqplot_Pendapatan_Tahunan_Miliar_IDR.png"/><a>*
  - *Interpretasi: Berdasarkan Q–Q plot, terlihat bahwa titik-titik data tidak sepenuhnya mengikuti garis lurus, terutama pada bagian kuantil rendah dan kuantil tinggi yang menyimpang cukup jauh dari garis referensi. Penyimpangan ini menunjukkan bahwa distribusi data tidak mengikuti distribusi normal. Pola lengkungan pada titik-titik data mengindikasikan adanya ketidaksimetrisan distribusi dan variasi nilai yang cukup besar, sehingga asumsi normalitas tidak terpenuhi. Hal ini sejalan dengan hasil uji Shapiro–Wilk yang sebelumnya menunjukkan bahwa data tidak terdistribusi normal.* 


### 5.3. Analisis Korelasi
- **Nilai Koefisien Korelasi:**
  - *Nilai r: 0.996*
  - *Interpretasi: Terdapat korelasi positif sangat kuat antara Pendapatan_Tahunan_Miliar_IDR dan Biaya_Akuisisi_Pelanggan_Juta_IDR. Artinya, semakin tinggi pendapatan tahunan, semakin tinggi pula biaya akuisisi pelanggan.* 

- **Visualisasi (Scatter Plot):**
  - *<a href="#"><img src="results/scatterplot_Pendapatan_Tahunan_Miliar_IDR_vs_Biaya_Akuisisi_Pelanggan_Juta_IDR.png"/><a>*
  - *Interpretasi: Pola pada scatter plot menunjukkan titik-titik data membentuk tren naik yang jelas dan rapat, sehingga mendukung hasil koefisien korelasi yang menunjukkan hubungan positif sangat kuat antara kedua variabel.* 


### 5.4. Analisis Regresi
- **Model Regresi:**
  - *Persamaan regresi: Pendapatan Tahunan Miliar IDR = −1,06 + 0,98 × Biaya Akuisisi Pelanggan Juta IDR*
  - *Interpretasi: Intercept (b0 = −1,06) menunjukkan nilai prediksi pendapatan tahunan ketika biaya akuisisi pelanggan bernilai 0. Nilai ini bersifat teoritis dan tidak terlalu bermakna secara praktis.
Slope (b1 = 0,98) berarti setiap kenaikan 1 juta IDR biaya akuisisi pelanggan diperkirakan akan meningkatkan pendapatan tahunan sebesar 0,98 miliar IDR. Ini menunjukkan hubungan positif antara kedua variabel.* 

- **Evaluasi Model (R-squared):**
  - *Nilai R-squared = 0.991*
  - *Interpretasi: Artinya, 99,1% variasi Pendapatan Tahunan dapat dijelaskan oleh Biaya Akuisisi Pelanggan melalui model regresi ini. Model memiliki kemampuan penjelasan yang sangat kuat.* 

- **Visualisasi (Garis Regresi pada Scatter Plot):**
  - *<a href="#"><img src="results/plot_regresi_Biaya_Akuisisi_Pelanggan_Juta_IDR_vs_Pendapatan_Tahunan_Miliar_IDR.png"/><a>*
  - *Interpretasi: Garis regresi secara jelas menunjukkan bahwa biaya akuisisi pelanggan merupakan faktor yang sangat berpengaruh terhadap pendapatan tahunan, dengan hubungan linear yang kuat dan konsisten.* 


---

## 6. Kesimpulan

Hasil analisis menunjukkan bahwa pendapatan tahunan startup memiliki variasi yang cukup besar, mencerminkan perbedaan skala bisnis antar startup dalam dataset. Meskipun data pendapatan tidak terdistribusi normal, analisis korelasi dan regresi menunjukkan adanya hubungan positif yang sangat kuat antara biaya akuisisi pelanggan dan pendapatan tahunan. Model regresi yang dibangun memiliki kemampuan penjelasan yang sangat tinggi, di mana 99,1% variasi pendapatan tahunan dapat dijelaskan oleh biaya akuisisi pelanggan. Wawasan utama dari analisis ini adalah bahwa biaya akuisisi pelanggan merupakan faktor yang sangat dominan dan berperan penting dalam meningkatkan pendapatan startup, meskipun faktor lain di luar model juga tetap perlu dipertimbangkan.
