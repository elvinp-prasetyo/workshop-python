Jupyter

Alat Project Jupyter tersedia untuk instalasi melalui Python Package Index, repositori perangkat lunak terkemuka yang dibuat untuk bahasa pemrograman Python.

JupyterLab

Instal JupyterLab dengan pip:

*pip install jupyterlab

Catatan: Jika Anda menginstal JupyterLab dengan conda atau mamba, sebaiknya gunakan saluran conda-forge.

Setelah terinstal, luncurkan JupyterLab dengan:

*jupyter-lab

Instal Jupyter Notebook  dengan pip:

Instal Jupyter Notebook klasik dengan:

*pip install notebook

Untuk menjalankan buku catatan:

*Jupyter Notebook

Memulai Server Notebook

Setelah Anda menginstal Jupyter Notebook di komputer Anda, Anda siap untuk menjalankan server notebook. Anda dapat memulai server notebook dari baris perintah (menggunakan Terminal di Mac/Linux, Command Prompt di Windows) dengan menjalankan:

buku catatan jupyter

Ini akan mencetak beberapa informasi tentang server notebook di terminal Anda, termasuk URL aplikasi web (secara default, http://localhost:8888):
Saat buku catatan dibuka di browser, Anda akan melihat Dasbor Buku Catatan, yang akan menampilkan daftar buku catatan, file, dan subdirektori di direktori tempat server buku catatan dimulai. Sebagian besar waktu, Anda ingin memulai server notebook di direktori tingkat tertinggi yang berisi notebook. Seringkali ini akan menjadi direktori home Anda.

Menggunakan antarmuka baris perintah

Notebook dapat dijalankan dari terminal menggunakan subperintah run. Ia mengharapkan jalur buku catatan sebagai argumen masukan dan menerima tanda opsional untuk mengubah perilaku default.

Menjalankan notebook semudah ini.

jupyter run notebook.ipynb

Anda dapat melewati lebih dari satu buku catatan juga.

jupyter run notebook.ipynb notebook2.ipynb

Secara default, kesalahan notebook akan dimunculkan dan dicetak ke terminal. Anda dapat menekannya dengan meneruskan tanda --allow-errors.

jupyter run notebook.ipynb --allow-errors