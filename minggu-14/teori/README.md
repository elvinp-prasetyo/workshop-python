An introduction to machine learning with scikit-learn
Section contents

Machine learning: pengaturan masalah
Secara umum, masalah pembelajaran mempertimbangkan satu set n sampel data dan kemudian mencoba memprediksi sifat data yang tidak diketahui. Jika setiap sampel lebih dari satu angka dan, misalnya, entri multidimensi (alias data multivariat), dikatakan memiliki beberapa atribut atau fitur.

Masalah yang terbagi dalam beberapa kategori:

klasifikasi: sampel milik dua atau lebih kelas dan kami ingin belajar dari data yang sudah berlabel bagaimana memprediksi kelas data yang tidak berlabel. Contoh masalah klasifikasi adalah pengenalan digit tulisan tangan, di mana tujuannya adalah untuk menetapkan setiap vektor input ke salah satu dari sejumlah kategori diskrit yang terbatas. Cara lain untuk memikirkan klasifikasi adalah sebagai bentuk pembelajaran terawasi diskrit (berlawanan dengan kontinu) di mana seseorang memiliki sejumlah kategori terbatas dan untuk masing-masing dari n sampel yang disediakan, salah satunya adalah mencoba memberi label dengan kategori atau kelas yang benar. .

regresi: jika output yang diinginkan terdiri dari satu atau lebih variabel kontinu, maka tugas tersebut disebut regresi. Contoh masalah regresi adalah prediksi panjang ikan salmon sebagai fungsi dari umur dan beratnya.

pembelajaran tanpa pengawasan, di mana data pelatihan terdiri dari satu set vektor input x tanpa nilai target yang sesuai. Tujuan dalam masalah tersebut mungkin untuk menemukan kelompok contoh serupa dalam data, yang disebut pengelompokan, atau untuk menentukan distribusi data dalam ruang input, yang dikenal sebagai estimasi kepadatan, atau untuk memproyeksikan data dari dimensi tinggi. ruang hingga dua atau tiga dimensi untuk tujuan visualisasi (Klik di sini untuk membuka halaman pembelajaran tanpa pengawasan Scikit-Learn).

Training set and testing set

Machine Learning mempelajari beberapa properti dari kumpulan data dan kemudian menguji properti tersebut terhadap kumpulan data lainnya. Praktik umum dalam pembelajaran mesin adalah mengevaluasi algoritme dengan membagi kumpulan data menjadi dua. salah satu set itu set pelatihan, di mana itu mempelajari beberapa properti; yang kedua menyebut set lainnya sebagai set pengujian, di mana dilakukan pengujian properti yang dipelajari.

Loading an example dataset
scikit-learn dilengkapi dengan beberapa kumpulan data standar, misalnya kumpulan data iris dan angka untuk klasifikasi dan kumpulan data diabetes untuk regresi.

Berikut ini, bahasa Python dari shell dan kemudian memuat set data iris dan digit dengan prompt juru bahasa Python:

$ python
>>> from sklearn import datasets
>>> iris = datasets.load_iris()
>>> digits = datasets.load_digits()

For instance, in the case of the digits dataset, digits.data gives access to the features that can be used to classify the digits samples:

Dataset adalah objek seperti kamus yang menyimpan semua data dan beberapa metadata tentang data tersebut. Data ini disimpan dalam anggota .data, yang merupakan array n_samples, n_features. Dalam kasus masalah yang diawasi, satu atau lebih variabel respons disimpan di anggota .target. Rincian lebih lanjut tentang kumpulan data yang berbeda dapat ditemukan di bagian khusus.

Misalnya, dalam kasus kumpulan data digit, digits.data memberikan akses ke fitur yang dapat digunakan untuk mengklasifikasikan sampel digit:

>>>
>>> print(digits.data)
[[ 0.   0.   5. ...   0.   0.   0.]
 [ 0.   0.   0. ...  10.   0.   0.]
 [ 0.   0.   0. ...  16.   9.   0.]
 ...
 [ 0.   0.   1. ...   6.   0.   0.]
 [ 0.   0.   2. ...  12.   0.   0.]
 [ 0.   0.  10. ...  12.   1.   0.]]
target memberikan kebenaran dasar untuk dataset digit, yaitu angka yang sesuai dengan setiap gambar digit yang kami coba pelajari:

>>>
>>> digits.target
array([0, 1, 2, ..., 8, 9, 8])
Shape of the data arrays

Data selalu berupa larik 2D, bentuk (n_samples, n_features), meskipun data aslinya mungkin memiliki bentuk yang berbeda. Dalam hal digit, setiap sampel asli adalah gambar bentuk (8, 8) dan dapat diakses menggunakan:
>>>
>>> digits.images[0]
array([[  0.,   0.,   5.,  13.,   9.,   1.,   0.,   0.],
       [  0.,   0.,  13.,  15.,  10.,  15.,   5.,   0.],
       [  0.,   3.,  15.,   2.,   0.,  11.,   8.,   0.],
       [  0.,   4.,  12.,   0.,   0.,   8.,   8.,   0.],
       [  0.,   5.,   8.,   0.,   0.,   9.,   8.,   0.],
       [  0.,   4.,  11.,   0.,   1.,  12.,   7.,   0.],
       [  0.,   2.,  14.,   5.,  10.,  12.,   0.,   0.],
       [  0.,   0.,   6.,  13.,  10.,   0.,   0.,   0.]])
Contoh sederhana pada dataset ini menggambarkan bagaimana mulai dari masalah awal seseorang dapat membentuk data untuk konsumsi di scikit-learn.

Learning and predicting

Dalam kasus kumpulan data digit, tugasnya adalah memprediksi, dengan diberikan gambar, digit mana yang diwakilinya. Kami diberikan sampel dari masing-masing 10 kelas yang mungkin (angka nol sampai sembilan) yang kami sesuaikan dengan estimator untuk dapat memprediksi kelas yang termasuk dalam sampel tak terlihat.

Dalam scikit-learn, estimator untuk klasifikasi adalah objek Python yang mengimplementasikan metode fit(X, y) dan predict(T).

Contoh estimator adalah kelas sklearn.svm.SVC, yang mengimplementasikan klasifikasi vektor pendukung. Konstruktor estimator mengambil parameter model sebagai argumen.

Untuk saat ini, kami akan mempertimbangkan estimator sebagai kotak hitam:

>>>
>>> from sklearn import svm
>>> clf = svm.SVC(gamma=0.001, C=100.)

Choosing the parameters of the model

Dalam contoh ini, kami mengatur nilai gamma secara manual. Untuk menemukan nilai yang baik untuk parameter ini, kita dapat menggunakan alat seperti pencarian grid dan validasi silang.

Contoh estimator clf (untuk pengklasifikasi) pertama-tama dipasang ke model; yaitu, ia harus belajar dari model. Ini dilakukan dengan meneruskan set pelatihan kami ke metode fit. Untuk set pelatihan, kami akan menggunakan semua gambar dari dataset kami, kecuali untuk gambar terakhir, yang akan kami simpan untuk prediksi kami. Kami memilih set pelatihan dengan sintaks [:-1] Python, yang menghasilkan array baru yang berisi semua kecuali item terakhir dari digits.data:

>>>
>>> clf.fit(digits.data[:-1], digits.target[:-1])
SVC(C=100.0, gamma=0.001)
Sekarang Anda dapat memprediksi nilai baru. Dalam hal ini, Anda akan memprediksi menggunakan gambar terakhir dari digits.data. Dengan memprediksi, Anda akan menentukan gambar dari set pelatihan yang paling cocok dengan gambar terakhir.

>>>
>>> clf.predict(digits.data[-1:])
array([8])
Gambar yang sesuai adalah:

../../_images/sphx_glr_plot_digits_last_image_001.png

Contoh lengkap dari masalah klasifikasi ini tersedia sebagai contoh yang dapat Anda jalankan dan pelajari: Mengenali digit tulisan tangan.

Konvensi
scikit-learn estimator mengikuti aturan tertentu untuk membuat perilaku mereka lebih prediktif. Ini dijelaskan secara lebih rinci dalam Daftar Istilah Umum dan Elemen API.

Ketik casting
Kecuali ditentukan lain, input akan dilemparkan ke float64:

>>>
>>> import numpy as np
>>> from sklearn import kernel_approximation

>>> rng = np.random.RandomState(0)
>>> X = rng.rand(10, 2000)
>>> X = np.array(X, dtype='float32')
>>> X.dtype
dtype('float32')

>>> transformer = kernel_approximation.RBFSampler()
>>> X_new = transformer.fit_transform(X)
>>> X_new.dtype
dtype('float64')
In this example, X is float32, which is cast to float64 by fit_transform(X).

Target regresi dilemparkan ke float64 dan target klasifikasi dipertahankan:

>>>
>>> from sklearn import datasets
>>> from sklearn.svm import SVC
>>> iris = datasets.load_iris()
>>> clf = SVC()
>>> clf.fit(iris.data, iris.target)
SVC()

>>> list(clf.predict(iris.data[:3]))
[0, 0, 0]

>>> clf.fit(iris.data, iris.target_names[iris.target])
SVC()

>>> list(clf.predict(iris.data[:3]))
['setosa', 'setosa', 'setosa']

Di sini, predict() pertama mengembalikan array integer, karena iris.target (array integer) digunakan sesuai. Predict() kedua mengembalikan array string, karena iris.target_names adalah untuk pemasangan.

Refitting and updating parameters
Hyper-parameter estimator dapat diperbarui setelah dibangun melalui metode set_params(). Memanggil fit() lebih dari sekali akan menimpa apa yang dipelajari oleh fit() sebelumnya:

>>>
>>> import numpy as np
>>> from sklearn.datasets import load_iris
>>> from sklearn.svm import SVC
>>> X, y = load_iris(return_X_y=True)

>>> clf = SVC()
>>> clf.set_params(kernel='linear').fit(X, y)
SVC(kernel='linear')
>>> clf.predict(X[:5])
array([0, 0, 0, 0, 0])

>>> clf.set_params(kernel='rbf').fit(X, y)
SVC()
>>> clf.predict(X[:5])
array([0, 0, 0, 0, 0])
Di sini, kernel default rbf pertama diubah menjadi linier melalui SVC.set_params() setelah estimator dibuat, dan diubah kembali ke rbf untuk memasang kembali estimator dan membuat prediksi kedua.

Pemasangan multikelas vs. multilabel
Saat menggunakan pengklasifikasi multikelas, tugas pembelajaran dan prediksi yang dilakukan bergantung pada format data target yang sesuai dengan:

>>>
>>> from sklearn.svm import SVC
>>> from sklearn.multiclass import OneVsRestClassifier
>>> from sklearn.preprocessing import LabelBinarizer

>>> X = [[1, 2], [2, 4], [4, 5], [3, 2], [3, 1]]
>>> y = [0, 0, 1, 1, 2]

>>> classif = OneVsRestClassifier(estimator=SVC(random_state=0))
>>> classif.fit(X, y).predict(X)
array([0, 0, 1, 1, 2])
Dalam kasus di atas, pengklasifikasi cocok pada larik 1d dari label multikelas dan oleh karena itu metode predict() memberikan prediksi multikelas yang sesuai. Dimungkinkan juga untuk menyesuaikan pada array 2d indikator label biner:

>>>
>>> y = LabelBinarizer().fit_transform(y)
>>> classif.fit(X, y).predict(X)
array([[1, 0, 0],
       [1, 0, 0],
       [0, 1, 0],
       [0, 0, 0],
       [0, 0, 0]])
Di sini, pengklasifikasi fit() pada representasi label biner 2d dari y, menggunakan LabelBinarizer. Dalam hal ini predict() mengembalikan larik 2d yang mewakili prediksi multilabel yang sesuai.

Perhatikan bahwa contoh keempat dan kelima mengembalikan semua nol, menunjukkan bahwa mereka tidak cocok dengan tiga label yang cocok. Dengan keluaran multilabel, sebuah instance juga dapat diberi beberapa label:

>>>
>>> from sklearn.preprocessing import MultiLabelBinarizer
>>> y = [[0, 1], [0, 2], [1, 3], [0, 2, 3], [2, 4]]
>>> y = MultiLabelBinarizer().fit_transform(y)
>>> classif.fit(X, y).predict(X)
array([[1, 1, 0, 0, 0],
       [1, 0, 1, 0, 0],
       [0, 1, 0, 1, 0],
       [1, 0, 1, 0, 0],
       [1, 0, 1, 0, 0]])
Dalam hal ini, pengklasifikasi cocok pada instance yang masing-masing diberi beberapa label. MultiLabelBinarizer digunakan untuk menggabungkan array 2d dari multilabel agar sesuai. Akibatnya, predict() mengembalikan larik 2d dengan beberapa label prediksi untuk setiap instance.

