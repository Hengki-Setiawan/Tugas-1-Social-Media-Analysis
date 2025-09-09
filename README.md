#### Tugas 1 Social Media Analysis

### Proyek Scraping Data Berita dan Media Sosial

Proyek ini dibuat untuk memenuhi tugas mata kuliah yang berfokus pada teknik pengumpulan data dari web (*web scraping*). Terdapat dua tugas utama: (1) Mengambil daftar berita dari portal berita `detik.com`, dan (2) Mengumpulkan data percakapan dari media sosial berdasarkan kata kunci "Prabowo".



### Tugas 1: Scraping Daftar Berita dari `detik.com`

# Latar Belakang Pemilihan `detik.com` 
Saya memilih **`detik.com`** untuk tugas pertama karena beberapa alasan:

* **Beritanya Banyak:** Sebagai situs berita besar, `detik.com` punya banyak sekali artikel di halaman depannya. Ini bagus untuk latihan karena data yang bisa diambil sangat beragam.
* **Strukturnya Rapi:** Halaman utama Detik menggunakan struktur HTML yang konsisten, di mana setiap "blok" berita dibungkus dalam tag `<article>`. Ini sangat mempermudah program untuk menemukan dan memilah-milah berita satu per satu.
* **Metadata yang Kaya:** Selain judul, setiap blok berita di halaman utama juga seringkali menyertakan ringkasan, nama penulis, dan waktu tayang, sesuai dengan syarat tugas untuk mengumpulkan metadata sebanyak mungkin.

# Penjelasan Rinci Alur Kode
Kode untuk tugas ini dirancang untuk "memborong" semua daftar berita yang ada di halaman utama `detik.com`. Berikut adalah cara kerjanya langkah demi langkah:

1.  **Persiapan Alat:**
    * **`requests`**: Digunakan untuk "mengunjungi" dan mengunduh halaman web `detik.com`. Saya juga menambahkan `headers` agar permintaan saya terlihat seperti browser biasa, bukan robot.
    * **`BeautifulSoup`**: Setelah halaman diunduh, library ini bertugas untuk "merapikan" kode HTML yang berantakan agar mudah dibaca dan dicari elemennya.
    * **`pandas`** & **`json`**: Digunakan di tahap akhir untuk menyusun semua data yang terkumpul ke dalam format tabel (untuk file **CSV** & **Excel**) dan format **JSON**.

2.  **Mengunjungi Halaman Utama:**
    Kode pertama kali mengakses URL `https://www.detik.com/`. Ini adalah halaman depan yang berisi puluhan tautan berita terbaru dan terpopuler.

3.  **Mencari Semua "Blok" Artikel:**
    Setelah halaman berhasil diunduh dan dirapikan, perintah `soup.find_all('article')` dijalankan untuk menyisir seluruh halaman dan mengumpulkan setiap "blok" berita.

4.  **"Membongkar" Setiap Blok Artikel (Looping):**
    Selanjutnya, kode melakukan perulangan untuk memeriksa setiap blok `<article>` satu per satu dan "mencopoti" informasi penting di dalamnya, seperti Judul (`title`), Tautan (`link`), Waktu Publikasi (`publication_time`), Penulis (`author`), URL Gambar (`image_url`), dan Ringkasan (`summary`).

5.  **Mengumpulkan ke dalam Satu Wadah:**
    Setiap set data dari satu artikel dibundel ke dalam sebuah *dictionary*, yang kemudian dimasukkan ke dalam sebuah *list* besar bernama `collected_data`.

6.  **Ekspor Hasil Panen:**
    Setelah semua data terkumpul, tahap terakhir adalah ekspor. Data di dalam `list` tadi diekspor menjadi tiga format berbeda: `.json`, `.csv`, dan `.xlsx` agar mudah diolah lebih lanjut.



### Tugas 2: Scraping Keyword "Prabowo" dari Media Sosial
# Latar Belakang Pemilihan Keyword "Prabowo" 

Untuk tugas kedua, saya memilih kata kunci **"Prabowo"** karena:

* **Signifikansi dan Relevansi Publik:** Sebagai Presiden Indonesia, Prabowo Subianto adalah figur publik yang selalu menjadi pusat perhatian dan perbincangan. Hal ini menjamin aliran data yang sangat besar dan konstan di media sosial.
* **Memenuhi Kebutuhan Volume Data:** Popularitas topik ini memudahkan pencapaian target minimal **1.000 baris data** seperti yang disyaratkan tugas.
* **Potensi Analisis yang Kaya:** Data percakapan publik ini sangat kaya akan opini. Ini membuka peluang besar untuk analisis lanjutan seperti analisis sentimen (positif, negatif, netral) atau pemetaan isu-isu kebijakan yang sedang ramai dibicarakan.

# Cara Kerja Menggunakan `Tweet Harvest` di Google Colab
Tugas kedua dieksekusi menggunakan *tool* **Tweet Harvest** di dalam lingkungan **Google Colaboratory**. Pendekatan ini dipilih karena praktis dan tidak memerlukan instalasi di komputer pribadi. Berikut alur kerjanya sesuai *notebook* yang dibuat:

1.  **Instalasi dan Setup:**
    Langkah pertama di dalam Colab adalah menginstal `Tweet Harvest` menggunakan perintah `npx`. Ini memastikan kita selalu menggunakan versi terbaru dari *tool* tersebut.

2.  **Konfigurasi Parameter Scraping:**
    Sebelum eksekusi, semua parameter yang dibutuhkan diatur dalam variabel Python agar mudah diubah:
    * **`filename`**: Nama file output diatur menjadi `'prabowo.csv'`.
    * **`search_keyword`**: Kata kunci pencarian utama diatur menjadi `'prabowo'`.
    * **`limit`**: Batas jumlah tweet yang ingin diambil diatur menjadi `1200` untuk memastikan target 1000 data terlampaui.
    * **`auth_token`**: Token autentikasi dimasukkan di sini. Token ini berfungsi sebagai kunci akses aman untuk masuk ke akun X (Twitter) tanpa harus menggunakan *username* dan *password* secara langsung di dalam kode.

3.  **Eksekusi Perintah Scraping:**
    Perintah inti dijalankan menggunakan `os.system()`. Kode ini secara dinamis menggabungkan semua variabel yang sudah diatur sebelumnya menjadi satu perintah terminal yang lengkap. Perintah inilah yang menyuruh `Tweet Harvest` untuk mulai bekerja: membuka browser virtual, melakukan pencarian, men-*scroll* halaman, dan "memanen" data.

4.  **Hasil Akhir:**
    Setelah proses selesai, `Tweet Harvest` secara otomatis menghasilkan file `prabowo.csv` di dalam lingkungan penyimpanan Google Colab. File ini berisi ribuan baris data tweet, lengkap dengan berbagai metadata berharga seperti isi tweet, *username*, waktu posting, jumlah *likes*, jumlah *retweet*, dan lainnya, yang siap untuk diunduh dan dianalisis.
