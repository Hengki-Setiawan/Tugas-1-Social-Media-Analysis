Tugas 1: Scraping Daftar Berita dari Portal Berita
Latar Belakang Pemilihan Portal Berita
Saya memilih dua portal berita populer, detik.com dan cnnindonesia.com, untuk tugas ini dengan beberapa pertimbangan strategis:

Struktur yang Mirip Namun Berbeda: Keduanya menggunakan tag <article> untuk membungkus setiap blok berita, yang menjadi titik awal yang baik untuk scraping. Namun, cara mereka menyajikan metadata (seperti penulis, kategori, dan waktu) sangat berbeda. Ini menjadi studi kasus yang bagus untuk menunjukkan bagaimana satu skrip dasar dapat diadaptasi untuk situs yang berbeda.

Kekayaan dan Variasi Data: Keduanya adalah situs berita besar dengan puluhan artikel di halaman depan. detik.com kaya akan metadata seperti penulis dan ringkasan, sementara cnnindonesia.com menonjolkan kategori berita. Mengambil data dari keduanya memberikan variasi data yang lebih menarik untuk dianalisis.

Penjelasan Rinci Alur Kode
Kode untuk tugas ini dirancang untuk "memborong" semua daftar berita yang ada di halaman utama kedua situs tersebut. Berikut adalah cara kerjanya secara umum, beserta adaptasi untuk tiap situs:

1. Persiapan Alat 
requests: Digunakan untuk "mengunjungi" dan mengunduh halaman web. Saya juga menambahkan headers agar permintaan saya terlihat seperti browser biasa, bukan robot.

BeautifulSoup: Setelah halaman diunduh, library ini bertugas untuk "merapikan" kode HTML agar mudah dibaca dan dicari elemennya.

pandas & json: Digunakan di tahap akhir untuk menyusun semua data yang terkumpul ke dalam format tabel (file CSV & Excel) dan format JSON.

2. Mengunjungi Halaman & Mencari Artikel 
Skrip akan mengakses URL target (baik Detik maupun CNN), kemudian perintah soup.find_all('article') dijalankan untuk menyisir seluruh halaman dan mengumpulkan setiap "blok" berita.

3. "Membongkar" Setiap Artikel (Adaptasi per Situs) 
Di sinilah penyesuaian utama terjadi. Meskipun prosesnya sama (melakukan perulangan untuk memeriksa setiap <article>), "resep" atau selector yang digunakan untuk mengambil data spesifik berbeda:

Untuk detik.com:

Judul: Dicari di dalam tag <h2> atau <h3> dengan kelas media__title.

Metadata: Informasi seperti publication_time, author, dan summary diambil dari tag <span> dan <p> dengan kelas spesifik mereka.

Untuk cnnindonesia.com:

Judul: Langsung dicari di dalam tag <h2>.

Metadata: Fokusnya adalah mengambil kategori dari tag <span> dengan kelas text-cnn_red. Metadata lain seperti penulis dan ringkasan tidak tersedia di halaman utama, sehingga diisi nilai default.

4. Mengumpulkan dan Mengekspor Hasil 
Setiap set data dari satu artikel (baik dari Detik maupun CNN) dibundel ke dalam sebuah dictionary, lalu dimasukkan ke dalam list besar collected_data. Terakhir, data ini diekspor menjadi tiga format berbeda: .json, .csv, dan .xlsx agar mudah diolah lebih lanjut.
