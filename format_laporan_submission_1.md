# Laporan Proyek Machine Learning Terapan - Akas Bagus Setiawan

## Domain Proyek

E-commerce telah menjadi bagian tak terpisahkan dari kehidupan modern dalam hal transaksi jual beli produk. Platform seperti Lazada menyediakan tempat bagi pelanggan untuk memberikan ulasan mengenai produk yang mereka beli. Ulasan ini sangat berharga bagi calon pembeli maupun penjual dalam menilai kualitas produk. Namun, dengan jumlah ulasan yang sangat besar, sulit bagi manusia untuk membaca dan memahami semua opini pelanggan secara manual. Oleh karena itu, dibutuhkan sistem otomatis yang dapat mengklasifikasikan sentimen dari ulasan pelanggan untuk membantu pengambilan keputusan.

**Rubrik/Kriteria Tambahan (Opsional)**:
- Mengapa ulasan produk sangat penting dalam dunia pasar moderen yang bersifat online? dikarenakan ulasan produk akan memberikan rekomendasi yang dapat menarik minat pembeli untuk menggunakan jasa atau produk tertentu dengan rating tertentu. pada zaman moderen ini influencer juga berpengaruh pada daya untuk menarik minat pembeli sehingga ada baiknya jika customer lebih memerhatikan ulasan produk terlebih dahulu dibandingkan influencer.
- Berdasarkan riset secara parsial maupun simultan variabel e- commerce, product review dan influencer secara bersama-sama berpengaruh terhadap keputusan pembelian melalui Marketplace Shopee. Saran yang dapat dikemukakan hendaknya konsumen berhati-hati untuk memilih penjual/seller, hendaknya masyarakat membaca dengan teliti mengenai rekomendasi yang diulas oleh konsumen yang telah membeli produk, hendaknya konsumen harus bijak menyikapi apakah produk yang dipromosikan influencer sesuai dengan kebutuhan.
  
Referensi: [Pengaruh E-Commerce, Product Review dan Influencer terhadap Keputusan Pembelian Melalui Marketplace Shopee (Studi Terhadap Masyarakat di Kampung Way Agung, Kabupaten Way Kanan)](https://jurnal.ubl.ac.id/index.php/jmv/article/view/3208) 

## Business Understanding

Pada bagian ini, kamu perlu menjelaskan proses klarifikasi masalah.

Bagian laporan ini mencakup:

### Problem Statements

Menjelaskan pernyataan masalah latar belakang:
- Bagaimana cara mengklasifikasikan ulasan pelanggan Lazada ke dalam kategori positif, negatif, dan netral?
-	Bagaimana performa berbagai algoritma Machine Learning dalam analisis sentimen ulasan pelanggan?


### Goals

Menjelaskan tujuan dari pernyataan masalah:
- Membangun model Machine Learning yang mampu mengklasifikasikan ulasan pelanggan secara otomatis.
-	Membandingkan performa berbagai model untuk menentukan model terbaik.


Semua poin di atas harus diuraikan dengan jelas. Anda bebas menuliskan berapa pernyataan masalah dan juga goals yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**:
- Menambahkan bagian “Solution Statement” yang menguraikan cara untuk meraih goals. Bagian ini dibuat dengan ketentuan sebagai berikut: 

    ### Solution statements
    - Menggunakan Naïve Bayes (NB), Support Vector Machine (SVM), dan Long Short-Term Memory (LSTM) untuk klasifikasi sentimen.
    - Menggunakan TF-IDF sebagai teknik ekstraksi fitur untuk model NB dan SVM
    - Menggunakan Tokenization & Embedding untuk LSTM agar dapat menangkap makna kontekstual dalam teks.
    - Melakukan evaluasi model menggunakan metrik akurasi, precision, recall, dan F1-score.

## Data Understanding
Paragraf awal bagian ini menjelaskan informasi mengenai data yang Anda gunakan dalam proyek. Sertakan juga sumber atau tautan untuk mengunduh dataset. Dataset yang digunakan berasal dari Kaggle: https://www.kaggle.com/datasets/grikomsn/lazada-indonesian-reviews?select=20191002-reviews.csv.

Selanjutnya uraikanlah seluruh variabel atau fitur pada data. Sebagai contoh:  

### Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
- Dataset ini berisi ulasan pelanggan terhadap produk di Lazada, dengan variable utama:
  1. reviewContent : Isi ulasan pelanggan.
  2. rating : Skor yang diberikan pelanggan (1-5).
  3. productName : Nama produk.
  4. reviewTime : Waktu ulasan dibuat.

**Rubrik/Kriteria Tambahan (Opsional)**:
- •	Jumlah Data: 21406 ulasan.
•	Kondisi Data: Terdapat nilai kosong yang perlu dihapus.
•	Distribusi Sentimen:
1. Positif (rating 4-5): Mayoritas ulasan.
2. Netral (rating 3): Lebih sedikit dibandingkan kategori lain.
3. Negatif (rating 1-2): Ulasan dengan keluhan pelanggan.

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menghapus nilai kosong: Menghilangkan ulasan yang tidak memiliki teks.
- Mengonversi rating ke sentimen:
  1. rating >= 4 → positive
  2. rating == 3 → neutral
  3. rating <= 2 → negative
-	Membersihkan teks:
  1. Konversi ke huruf kecil.
  2. Menghapus karakter khusus, angka, dan tanda baca.
-	Membagi data menjadi training dan testing set (80% training, 20% testing).
-	TF-IDF Vectorization untuk model NB dan SVM.
-	Tokenization & Padding untuk model LSTM.

- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.
1. Mengatasi Missing Values, Beberapa kolom dalam dataset memiliki nilai kosong (misalnya reviewTitle dan reviewContent). Jika tidak ditangani, model dapat mengalami kesalahan atau menghasilkan prediksi yang tidak akurat. Oleh karena itu, dilakukan penghapusan data yang tidak memiliki reviewContent karena ulasan adalah fitur utama dalam analisis sentimen.
Mengonversi Tipe Data
2. Kolom rating, awalnya berbentuk numerik dengan tipe data yang tidak sesuai. Oleh karena itu, dilakukan konversi ke tipe data integer agar lebih mudah digunakan dalam klasifikasi sentimen.
3. Labeling Sentimen, Data ulasan tidak memiliki label sentimen secara eksplisit. Oleh karena itu, perlu dilakukan transformasi rating menjadi tiga kategori sentimen:
   a. Positive (rating 4-5)
   b. Neutral (rating 3)
   c. Negative (rating 1-2)
Labeling ini diperlukan agar model dapat memahami hubungan antara ulasan dan sentimen yang sesuai.
4. Membersihkan Teks (Text Cleaning), Data teks dari ulasan sering mengandung karakter yang tidak relevan seperti simbol, angka, dan tanda baca. Oleh karena itu, dilakukan pembersihan teks agar model lebih fokus pada kata-kata yang bermakna dalam analisis sentimen.
5. Transformasi Teks ke Representasi Numerik, Model machine learning tidak dapat memproses teks secara langsung, sehingga dilakukan transformasi teks ke dalam bentuk numerik menggunakan TF-IDF untuk model berbasis statistik (Naïve Bayes & SVM) dan Tokenization + Padding untuk model berbasis deep learning (LSTM).
6. Pembagian Data (Train-Test Split), Untuk menghindari overfitting dan menguji kinerja model secara objektif, dataset dibagi menjadi dua bagian:
   a. Training Set (80%): Digunakan untuk melatih model
   b. Testing Set (20%): Digunakan untuk menguji performa model pada data yang belum pernah dilihat sebelumnya

## Modeling
Tahapan ini membahas mengenai model machine learning yang digunakan untuk menyelesaikan permasalahan. Anda perlu menjelaskan tahapan dan parameter yang digunakan pada proses pemodelan.
Model yang digunakan:
•	Naïve Bayes (NB): Model probabilistik berbasis TF-IDF.
•	Support Vector Machine (SVM): Model klasifikasi berbasis hyperplane optimal.
•	Long Short-Term Memory (LSTM): Model deep learning berbasis RNN untuk menangkap konteks dalam teks.


**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan kelebihan dan kekurangan dari setiap algoritma yang digunakan.
  - Naïve Bayes: Kelebihan	Cepat dan sederhana, Kekurangan	Kurang akurat untuk teks kompleks
  - SVM: Kelebihan Akurat dalam data terbatas, Kekurangan Waktu komputasi lebih lama
  - LSTM: Kelebihan	Memahami konteks kalimat, Kekurangan Membutuhkan lebih banyak data dan komputasi

- Jika menggunakan satu algoritma pada solution statement, lakukan proses improvement terhadap model dengan hyperparameter tuning. **Jelaskan proses improvement yang dilakukan**.
- Jika menggunakan dua atau lebih algoritma pada solution statement, maka pilih model terbaik sebagai solusi. **Jelaskan mengapa memilih model tersebut sebagai model terbaik**.
- Model terbaik dipilih berdasarkan evaluasi metrik. SVM memiliki akurasi tertinggi (97%) dengan keseimbangan precision, recall, dan F1-score yang baik

## Evaluation
Pada bagian ini anda perlu menyebutkan metrik evaluasi yang digunakan. Lalu anda perlu menjelaskan hasil proyek berdasarkan metrik evaluasi yang digunakan.

Saya memiih kasus klasifikasi dan menggunakan metrik **akurasi, precision, recall, dan F1 score**. Jelaskan mengenai beberapa hal berikut:
- Accuracy: Persentase prediksi yang benar
- Precision: Proporsi prediksi positif yang benar.
- Recall: Kemampuan model mendeteksi kategori tertentu.
- F1-Score: Rata-rata harmonik antara precision dan recall

- Menjelaskan hasil proyek berdasarkan metrik evaluasi
1. Naïve Bayes: Accuracy 90%, Precision 90%, Recall 90%, F1-Score 87%
2. SVM: Accuracy 97%, Precision 97%, Recall97%, F1-Score 97%
3. LSTM: Accuracy 96%, Precision 96%, Recall 96%, F1-Score 96%
Dari hasil evaluasi, SVM adalah model terbaik dengan akurasi dan F1-score tertinggi. Model ini dapat digunakan untuk mengotomatisasi analisis sentimen pada ulasan pelanggan Lazada dengan tingkat akurasi yang sangat tinggi.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.

