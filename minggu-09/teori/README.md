12. Virtual Environments and Packages
12.1. Introduction

Aplikasi Python akan sering menggunakan paket dan modul yang tidak datang sebagai bagian dari perpustakaan standar. Aplikasi terkadang memerlukan versi pustaka tertentu, karena aplikasi mungkin mengharuskan bug tertentu telah diperbaiki atau aplikasi dapat ditulis menggunakan versi antarmuka pustaka yang sudah usang.

Ini berarti satu instalasi Python untuk memenuhi persyaratan setiap aplikasi. Jika aplikasi A membutuhkan versi 1.0 dari modul tertentu tetapi aplikasi B membutuhkan versi 2.0, maka persyaratan tersebut bertentangan dan menginstal versi 1.0 atau 2.0 akan membuat satu aplikasi tidak dapat berjalan.

Solusi untuk masalah ini adalah membuat lingkungan virtual, pohon direktori mandiri yang berisi instalasi Python untuk versi Python tertentu, ditambah sejumlah paket tambahan.

12.2. Creating Virtual Environments

 Modul yang digunakan untuk membuat dan mengelola lingkungan virtual disebut venv. venv biasanya akan menginstal versi terbaru dari Python yang tersedia.

Untuk membuat lingkungan virtual, tentukan direktori untuk tempat meletakkannya, dan jalankan modul venv sebagai skrip dengan path:

python3 -m venv tutorial-env

Ini akan membuat direktori tutorial-env jika tidak ada, dan juga membuat direktori di dalamnya yang berisi salinan interpreter Python dan berbagai file pendukung.

Lokasi direktori umum untuk lingkungan virtual adalah .venv. Nama ini membuat direktori biasanya tersembunyi di shell Anda dan dengan demikian menyingkir sambil memberinya nama yang menjelaskan mengapa direktori itu ada. Ini juga mencegah bentrokan dengan file definisi variabel lingkungan .env yang didukung oleh beberapa perkakas.

Setelah Anda membuat lingkungan virtual, Anda dapat mengaktifkannya.

On Windows, run:

tutorial-env\Scripts\activate.bat

On Unix or MacOS, run:

source tutorial-env/bin/activate

(Skrip ini ditulis untuk bash shell. Jika Anda menggunakan csh atau cangkang ikan, ada alternatif skrip Activate.csh dan Activate.fish yang harus Anda gunakan.)

Mengaktifkan lingkungan virtual akan mengubah prompt shell Anda untuk menunjukkan lingkungan virtual apa yang Anda gunakan, dan memodifikasi lingkungan sehingga menjalankan python akan memberi Anda versi tertentu dan instalasi Python. Sebagai contoh:

$ source ~/envs/tutorial-env/bin/activate
(tutorial-env) $ python
Python 3.5.1 (default, May  6 2016, 10:59:36)
  ...
>>> import sys
>>> sys.path
['', '/usr/local/lib/python35.zip', ...,
'~/envs/tutorial-env/lib/python3.5/site-packages']
>>>

12.3. Managing Packages with pip

Anda dapat menginstal, memutakhirkan, dan menghapus paket menggunakan program bernama pip. Secara default pip akan menginstal paket dari Python Package Index, <https://pypi.org>. Anda dapat menelusuri Indeks Paket Python dengan membukanya di browser web Anda.

pip memiliki sejumlah sub-perintah: “install”, “uninstall”, “freeze”, dll. (Lihat panduan Instalasi Modul Python untuk dokumentasi lengkap untuk pip.)

Anda dapat menginstal versi terbaru dari sebuah paket dengan menentukan nama paket:

(tutorial-env) $ python -m pip install novas
Collecting novas
  Downloading novas-3.1.1.3.tar.gz (136kB)
Installing collected packages: novas
  Running setup.py install for novas
Successfully installed novas-3.1.1.3

Anda juga dapat menginstal versi paket tertentu dengan memberikan nama paket diikuti dengan == dan nomor versi:

(tutorial-env) $ python -m pip install requests==2.6.0
Collecting requests==2.6.0
  Using cached requests-2.6.0-py2.py3-none-any.whl
Installing collected packages: requests
Successfully installed requests-2.6.0

Jika Anda menjalankan kembali perintah ini, pip akan melihat bahwa versi yang diminta sudah diinstal dan tidak melakukan apa pun. Anda dapat memberikan nomor versi yang berbeda untuk mendapatkan versi itu, atau Anda dapat menjalankan pip install --upgrade untuk memutakhirkan paket ke versi terbaru:

(tutorial-env) $ python -m pip install --upgrade requests
Collecting requests
Installing collected packages: requests
  Found existing installation: requests 2.6.0
    Uninstalling requests-2.6.0:
      Successfully uninstalled requests-2.6.0
Successfully installed requests-2.7.0

pip uninstall diikuti oleh satu atau lebih nama paket akan menghapus paket dari lingkungan virtual.

pip show akan menampilkan informasi tentang paket tertentu:

(tutorial-env) $ pip show requests
---
Metadata-Version: 2.0
Name: requests
Version: 2.7.0
Summary: Python HTTP for Humans.
Home-page: http://python-requests.org
Author: Kenneth Reitz
Author-email: me@kennethreitz.com
License: Apache 2.0
Location: /Users/akuchling/envs/tutorial-env/lib/python3.4/site-packages
Requires:

pip list akan menampilkan semua paket yang diinstal di lingkungan virtual:

(tutorial-env) $ pip list
novas (3.1.1.3)
numpy (1.9.2)
pip (7.0.3)
requests (2.7.0)
setuptools (16.0)

pip freeze akan menghasilkan daftar serupa dari paket yang diinstal, tetapi outputnya menggunakan format yang diharapkan oleh pip install. Konvensi umum adalah meletakkan daftar ini dalam file requirements.txt:

(tutorial-env) $ pip freeze > requirements.txt
(tutorial-env) $ cat requirements.txt
novas==3.1.1.3
numpy==1.9.2
requests==2.7.0

persyaratan.txt kemudian dapat dikomit ke kontrol versi dan dikirimkan sebagai bagian dari aplikasi. Pengguna kemudian dapat menginstal semua paket yang diperlukan dengan install -r:

(tutorial-env) $ python -m pip install -r requirements.txt
Collecting novas==3.1.1.3 (from -r requirements.txt (line 1))
  ...
Collecting numpy==1.9.2 (from -r requirements.txt (line 2))
  ...
Collecting requests==2.7.0 (from -r requirements.txt (line 3))
  ...
Installing collected packages: novas, numpy, requests
  Running setup.py install for novas
Successfully installed novas-3.1.1.3 numpy-1.9.2 requests-2.7.0

pip memiliki lebih banyak opsi. Lihat panduan Instalasi Modul Python untuk dokumentasi lengkap untuk pip. Ketika Anda telah menulis sebuah paket dan ingin membuatnya tersedia di Python Package Index, lihat panduan Mendistribusikan Modul Python.

Getting started with conda

Conda adalah pengelola paket dan pengelola lingkungan andal yang Anda gunakan dengan perintah baris perintah di Anaconda Prompt untuk Windows, atau di jendela terminal untuk macOS atau Linux.

Panduan 20 menit untuk memulai dengan conda ini memungkinkan Anda mencoba fitur utama conda. Anda harus memahami cara kerja conda ketika Anda menyelesaikan panduan ini.

Sebelum Anda mulai

Anda seharusnya sudah menginstal Anaconda.

Mulai conda

Windows

   Dari menu Mulai, cari dan buka "Anaconda Prompt." Di Windows, semua perintah diketik ke dalam jendela Anaconda Prompt.

Mengelola conda

Verifikasi bahwa conda diinstal dan berjalan di sistem Anda dengan mengetik:

    conda --version

Conda menampilkan nomor versi yang telah Anda instal. Anda tidak perlu menavigasi ke direktori Anaconda.

Perbarui conda ke versi saat ini. Ketik berikut ini:

    conda update conda

Conda membandingkan versi dan kemudian menampilkan apa yang tersedia untuk diinstal.

Jika versi conda yang lebih baru tersedia, ketik y untuk memperbarui:

    Proceed ([y]/n)? y

Mengelola lingkungan

Buat lingkungan baru dan instal paket di dalamnya.

Kami akan memberi nama kepingan salju lingkungan dan menginstal paket BioPython. Di Anaconda Prompt atau di jendela terminal Anda, ketikkan yang berikut ini:

conda create --name snowflakes biopython

Conda memeriksa untuk melihat paket tambahan ("dependencies") apa yang dibutuhkan BioPython, dan menanyakan apakah Anda ingin melanjutkan:

Proceed ([y]/n)? y
Ketik "y" dan tekan Enter untuk melanjutkan.

Untuk menggunakan, atau "mengaktifkan" lingkungan baru, ketik berikut ini:

    Windows: conda activate snowflakes

    macOS and Linux: conda activate snowflakes
Untuk melihat daftar semua lingkungan Anda, ketik:

conda info --envs

Daftar lingkungan muncul, mirip dengan berikut ini:

conda environments:

    base           /home/username/Anaconda3
    snowflakes   * /home/username/Anaconda3/envs/snowflakes

Mengelola Python

Buat lingkungan baru bernama "snakes" yang berisi Python 3.9:

conda create --name snakes python=3.9

Ketika conda bertanya apakah Anda ingin melanjutkan, ketik "y" dan tekan Enter.

Aktifkan lingkungan baru:

    Windows: conda activate snakes

    macOS and Linux: conda activate snakes

Verifikasi bahwa lingkungan snakes telah ditambahkan dan aktif:

conda info --envs

Conda menampilkan daftar semua lingkungan dengan tanda bintang (*) setelah nama lingkungan aktif:

# conda environments:
#
base                     /home/username/anaconda3
snakes                *  /home/username/anaconda3/envs/snakes
snowflakes               /home/username/anaconda3/envs/snowflakes


Lingkungan aktif juga ditampilkan di depan prompt Anda di (parentheses) atau [brackets] seperti ini:
(snakes) $

Verifikasi versi Python mana yang ada di lingkungan Anda saat ini:

python --version


Mengelola paket

Di bagian ini, Anda memeriksa paket mana yang telah Anda instal, memeriksa mana yang tersedia dan mencari paket tertentu dan menginstalnya.



  Untuk menemukan paket yang telah Anda instal, aktifkan terlebih dahulu lingkungan yang ingin Anda cari. Lihat di atas untuk perintah untuk mengaktifkan lingkungan ular Anda.

     Periksa untuk melihat apakah paket yang belum Anda instal bernama "beautifulsoup4" tersedia dari repositori Anaconda (harus terhubung ke Internet):

    conda search beautifulsoup4

    Conda menampilkan daftar semua paket dengan nama itu di repositori Anaconda, jadi kami tahu itu tersedia.

    Instal paket ini ke lingkungan saat ini:

    conda install beautifulsoup4

    Periksa untuk melihat apakah program yang baru diinstal ada di lingkungan ini:

    conda list

