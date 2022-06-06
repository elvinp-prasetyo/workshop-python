Pandas

pandas adalah perpustakaan perangkat lunak yang ditulis untuk bahasa pemrograman Python untuk manipulasi dan analisis data. Secara khusus, ia menawarkan struktur data dan operasi untuk memanipulasi tabel numerik dan deret waktu. Ini adalah perangkat lunak gratis yang dirilis di bawah lisensi BSD tiga klausa.

Series

Series adalah array berlabel satu dimensi yang mampu menampung semua tipe data (bilangan bulat, string, angka floating point, objek Python, dll.). Label sumbu secara kolektif disebut sebagai indeks.

DataFrame

DataFrame adalah struktur data berlabel 2 dimensi dengan kolom dari jenis yang berpotensi berbeda. Anda dapat menganggapnya seperti spreadsheet atau tabel SQL, atau dict objek Seri. Ini umumnya objek panda yang paling umum digunakan. Seperti Seri, DataFrame menerima berbagai jenis input:

    Dikt dari ndarrays 1D, daftar, dikte, atau Seri

    2-D numpy.ndarray

    Terstruktur atau rekam ndarray

    Seri A

    DataFrame lain

Bersama dengan data, Anda dapat secara opsional meneruskan argumen indeks (label baris) dan kolom (label kolom). Jika Anda melewati indeks dan/atau kolom, Anda menjamin indeks dan/atau kolom dari DataFrame yang dihasilkan. Dengan demikian, dict of Series plus indeks tertentu akan membuang semua data yang tidak cocok dengan indeks yang diteruskan.

Jika label sumbu tidak diteruskan, label akan dibuat dari data input berdasarkan aturan akal sehat.

Descriptive statistics

Terdapat sejumlah besar metode untuk menghitung Descriptive statistics dan operasi terkait lainnya pada Seri, DataFrame. Sebagian besar dari ini adalah agregasi (sehingga menghasilkan hasil dimensi yang lebih rendah) seperti sum(), mean(), dan quantile(), tetapi beberapa di antaranya, seperti cumsum() dan cumprod(), menghasilkan objek dengan ukuran yang sama.

Reindexing and altering labels

reindex() adalah metode penyelarasan data mendasar di pandas. Ini digunakan untuk mengimplementasikan hampir semua fitur lain yang mengandalkan fungsionalitas perataan label. Mengindeks ulang berarti menyesuaikan data agar sesuai dengan sekumpulan label tertentu di sepanjang sumbu tertentu. Ini menyelesaikan beberapa hal:

    Menyusun ulang data yang ada agar sesuai dengan kumpulan label baru

    Menyisipkan penanda nilai yang hilang (NA) di lokasi label yang tidak memiliki data untuk label tersebut

    Jika ditentukan, isi data untuk label yang hilang menggunakan logika (sangat relevan untuk bekerja dengan data deret waktu)

dtypes

Untuk sebagian besar, panda menggunakan array NumPy dan dtypes untuk Seri atau kolom individual dari DataFrame. NumPy menyediakan dukungan untuk float, int, bool, timedelta64[ns] dan datetime64[ns] (perhatikan bahwa NumPy tidak mendukung datetimes yang sadar zona waktu).

panda dan perpustakaan pihak ketiga memperluas sistem tipe NumPy di ​​beberapa tempat. Bagian ini menjelaskan ekstensi yang dibuat panda secara internal. Lihat Jenis ekstensi untuk cara menulis ekstensi Anda sendiri yang berfungsi dengan panda. Lihat dtypesata ekstensi untuk daftar pustaka pihak ketiga yang telah menerapkan ekstensi.

Tabel berikut mencantumkan semua jenis ekstensi pandas. Untuk metode yang membutuhkan argumen dtype, string dapat ditentukan seperti yang ditunjukkan. Lihat bagian dokumentasi masing-masing untuk mengetahui lebih lanjut tentang setiap jenis.

lima perintah yang ada di pandas

mean()

mean() digunakan untuk menghitung nilai rata-rata dari sebuah kolom numerik di dataframe.

isna()

isna() digunakan untuk mengecek apakah ada nilai NaN pada dataframe. Function ini akan mengembalikan nilai Boolean, True atau False, untuk tiap elemen di dataframe. Kita juga dapat menambahkan function any() untuk mengecek nilai NaN berdasarkan kolom.

loc

loc digunakan untuk mengakses data berdasarkan label (nama kolom).

dtypes

dtypes digunakan untuk mengecek tipe data untuk tiap kolom di dataframe. Bisa juga digunakan untuk mengecek tipe data salah satu kolom.

head()

head() digunakan untuk menampilkan data awal atau data teratas pada dataframe. Default-nya jika kita tidak memberikan argumen di dalam tanda kurung (), data yang akan ditampilkan adalah 5 baris teratas. Namun, kita juga dapat menentukan berapa baris data yang ingin ditampilkan dengan memberikan argumen berupa bilangan integer.
