10. Brief Tour of the Standard Library

10.1. Operating System Interface

Modul os menyediakan beberapa fungsi untuk berinteraksi dengan sistem operasi di bawah ini:


>>> import os
>>> os.getcwd()      # Return the current working directory
'C:\\Python310'
>>> os.chdir('/server/accesslogs')   # Change current working directory
>>> os.system('mkdir today')   # Run the command mkdir in the system shell
0

Fungsi built-in dir() dan help() berguna sebagai bantuan interaktif untuk bekerja dengan modul os:


>>> import os
>>> dir(os)
<returns a list of all module functions>
>>> help(os)
<returns an extensive manual page created from the module's docstrings>

Untuk tugas manajemen file dan direktori harian, modul shutil digunakan:


>>> import shutil
>>> shutil.copyfile('data.db', 'archive.db')
'archive.db'
>>> shutil.move('/build/executables', 'installdir')
'installdir'

10.2. File Wildcards

Modul glob menyediakan fungsi untuk membuat daftar file dari pencarian wildcard direktori:


>>> import glob
>>> glob.glob('*.py')
['primes.py', 'random.py', 'quote.py']

10.3. Command Line Arguments

Argumen ini disimpan dalam atribut argv modul sys sebagai daftar. Misalnya hasil keluaran berikut dari menjalankan python demo.py satu dua tiga di baris perintah berikut ini:
>>>

>>> import sys
>>> print(sys.argv)
['demo.py', 'one', 'two', 'three']

10.4. Error Output Redirection and Program Termination

Modul sys juga memiliki atribut untuk stdin, stdout, dan stderr. Yang terakhir ini berguna untuk memancarkan peringatan dan pesan kesalahan agar terlihat bahkan ketika stdout telah dialihkan.
contoh :


>>> sys.stderr.write('Warning, log file not found starting a new one\n')
Warning, log file not found starting a new one

Cara paling mudah untuk menghentikan skrip ini adalah dengan menggunakan sys.exit().
10.5. String Pattern Matching

Modul re menyediakan alat ekspresi reguler untuk pemrosesan string tingkat lanjut. Untuk pencocokan dan manipulasi yang kompleks, ekspresi reguler menawarkan solusi yang ringkas dan dioptimalkan:

>>> import re
>>> re.findall(r'\bf[a-z]*', 'which foot or hand fell fastest')
['foot', 'fell', 'fastest']
>>> re.sub(r'(\b[a-z]+) \1', r'\1', 'cat in the the hat')
'cat in the hat'

10.6. Mathematics

Modul matematika memberikan akses ke fungsi pustaka C yang mendasari untuk matematika titik mengambang:
>>>

>>> import math
>>> math.cos(math.pi / 4)
0.70710678118654757
>>> math.log(1024, 2)
10.0


10.7. Internet Access

modul untuk mengakses internet dan memproses protokol internet yang paling sederhana adalah urllib.request untuk mengambil data dari URL dan smtplib untuk mengirim email seperti di bawah ini:

>>> from urllib.request import urlopen
>>> with urlopen('http://worldtimeapi.org/api/timezone/etc/UTC.txt') as response:
...     for line in response:
...         line = line.decode()             # Convert bytes to a str
...         if line.startswith('datetime'):
...             print(line.rstrip())         # Remove trailing newline
...
datetime: 2022-01-01T01:36:47.689215+00:00

>>> import smtplib
>>> server = smtplib.SMTP('localhost')
>>> server.sendmail('soothsayer@example.org', 'jcaesar@example.org',
... """To: jcaesar@example.org
... From: soothsayer@example.org
...
... Beware the Ides of March.
... """)
>>> server.quit()


10.8. Dates and Times

Modul datetime menyediakan kelas untuk memanipulasi tanggal dan waktu dengan cara yang sederhana dan kompleks dan juga mendukung objek yang sadar zona waktu.
contoh :

>>> # dates are easily constructed and formatted
>>> from datetime import date
>>> now = date.today()
>>> now
datetime.date(2003, 12, 2)
>>> now.strftime("%m-%d-%y. %d %b %Y is a %A on the %d day of %B.")
'12-02-03. 02 Dec 2003 is a Tuesday on the 02 day of December.'

>>> # dates support calendar arithmetic
>>> birthday = date(1964, 7, 31)
>>> age = now - birthday
>>> age.days
14368

10.9. Data Compression

Pengarsipan data umum dan format kompresi secara langsung didukung oleh modul termasuk: zlib, gzip, bz2, lzma, zipfile dan tarfile.
contoh :

>>> import zlib
>>> s = b'witch which has which witches wrist watch'
>>> len(s)
41
>>> t = zlib.compress(s)
>>> len(t)
37
>>> zlib.decompress(t)
b'witch which has which witches wrist watch'
>>> zlib.crc32(s)
226805979

10.10. Performance Measurement

Modul timeit dengan cepat menunjukkan keunggulan kinerja yang  sederhana.
contoh :

>>> from timeit import Timer
>>> Timer('t=a; a=b; b=t', 'a=1; b=2').timeit()
0.57535828626024577
>>> Timer('a,b = b,a', 'a=1; b=2').timeit()
0.54962537085770791


10.11. Quality Control

Modul doctest menyediakan alat untuk memindai modul dan memvalidasi tes yang tertanam dalam docstrings program. Konstruksi pengujian sesederhana memotong dan menempelkan panggilan biasa beserta hasilnya ke dalam docstring. Ini meningkatkan dokumentasi dengan memberikan contoh kepada pengguna dan memungkinkan modul doctest untuk memastikan kode tetap sesuai dengan dokumentasi.
contoh :

def average(values):
    """Computes the arithmetic mean of a list of numbers.

    >>> print(average([20, 30, 70]))
    40.0
    """
    return sum(values) / len(values)

import doctest
doctest.testmod()   # automatically validate the embedded tests

Modul unittest tidak semudah modul doctest, tetapi memungkinkan serangkaian tes yang lebih komprehensif untuk dipertahankan dalam file terpisah
contoh :

import unittest

class TestStatisticalFunctions(unittest.TestCase):

    def test_average(self):
        self.assertEqual(average([20, 30, 70]), 40.0)
        self.assertEqual(round(average([1, 5, 7]), 1), 4.3)
        with self.assertRaises(ZeroDivisionError):
            average([])
        with self.assertRaises(TypeError):
            average(20, 30, 70)

unittest.main()  # Calling from the command line invokes all tests

10.12. Batteries Included

Modul xmlrpc.client dan xmlrpc.server membuat penerapan panggilan prosedur jarak jauh menjadi tugas yang hampir sepele. Terlepas dari nama modul, tidak ada pengetahuan langsung atau penanganan XML yang diperlukan.


11. Brief Tour of the Standard Library — Part II

Modul Lanjutan ini mencakup modul yang lebih canggih yang mendukung kebutuhan pemrograman profesional. Modul ini jarang muncul dalam skrip kecil
11.1. Output Formatting

Modul reprlib menyediakan versi repr() yang disesuaikan untuk tampilan singkat container besar atau bersarang dalam:
>>>

>>> import reprlib
>>> reprlib.repr(set('supercalifragilisticexpialidocious'))
"{'a', 'c', 'd', 'e', 'f', 'g', ...}"

Modul pprint menawarkan kontrol yang lebih canggih atas pencetakan objek bawaan dan objek yang ditentukan pengguna dengan cara yang dapat dibaca oleh penerjemah:
>>>

>>> import pprint
>>> t = [[[['black', 'cyan'], 'white', ['green', 'red']], [['magenta',
...     'yellow'], 'blue']]]
...
>>> pprint.pprint(t, width=30)
[[[['black', 'cyan'],
   'white',
   ['green', 'red']],
  [['magenta', 'yellow'],
   'blue']]]

Modul textwrap memformat paragraf teks agar sesuai dengan lebar layar yang diberikan:
>>>

>>> import textwrap
>>> doc = """The wrap() method is just like fill() except that it returns
... a list of strings instead of one big string with newlines to separate
... the wrapped lines."""
...
>>> print(textwrap.fill(doc, width=40))
Metode wrap() sama seperti fill()
kecuali itu mengembalikan daftar string
alih-alih satu string besar dengan baris baru
untuk memisahkan garis yang dibungkus.

11.2. Templating

Modul string menyertakan kelas Template dengan sintaks yang disederhanakan yang cocok untuk diedit oleh pengguna akhir. Hal ini memungkinkan pengguna untuk menyesuaikan aplikasi mereka tanpa harus mengubah aplikasi.

contoh :

>>> from string import Template
>>> t = Template('${village}folk send $$10 to $cause.')
>>> t.substitute(village='Nottingham', cause='the ditch fund')
'Nottinghamfolk send $10 to the ditch fund.'

11.4. Multi-threading

Threading adalah teknik untuk memisahkan tugas yang tidak bergantung secara berurutan. Threads dapat digunakan untuk meningkatkan daya tanggap aplikasi yang menerima masukan pengguna saat tugas lain berjalan di latar belakang. 

Kode berikut menunjukkan bagaimana modul threading tingkat tinggi dapat menjalankan tugas di latar belakang sementara program utama terus berjalan:

import threading, zipfile

class AsyncZip(threading.Thread):
    def __init__(self, infile, outfile):
        threading.Thread.__init__(self)
        self.infile = infile
        self.outfile = outfile

    def run(self):
        f = zipfile.ZipFile(self.outfile, 'w', zipfile.ZIP_DEFLATED)
        f.write(self.infile)
        f.close()
        print('Finished background zip of:', self.infile)

background = AsyncZip('mydata.txt', 'myarchive.zip')
background.start()
print('The main program continues to run in foreground.')

background.join()    # Wait for the background task to finish
print('Main program waited until background was done.')

11.5. Logging

Modul logging menawarkan sistem logging berfitur lengkap dan fleksibel. Paling sederhana, pesan log dikirim ke file atau ke sys.stderr
contoh :

import logging
logging.debug('Debugging information')
logging.info('Informational message')
logging.warning('Warning:config file %s not found', 'server.conf')
logging.error('Error occurred')
logging.critical('Critical error -- shutting down')

This produces the following output:

WARNING:root:Warning:config file server.conf not found
ERROR:root:Error occurred
CRITICAL:root:Critical error -- shutting down

11.6. Weak References

 Modul weakref menyediakan alat untuk melacak objek tanpa membuat referensi. 
 contoh :


>>> import weakref, gc
>>> class A:
...     def __init__(self, value):
...         self.value = value
...     def __repr__(self):
...         return str(self.value)
...
>>> a = A(10)                   # create a reference
>>> d = weakref.WeakValueDictionary()
>>> d['primary'] = a            # does not create a reference
>>> d['primary']                # fetch the object if it is still alive
10
>>> del a                       # remove the one reference
>>> gc.collect()                # run garbage collection right away
0
>>> d['primary']                # entry was automatically removed
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
    d['primary']                # entry was automatically removed
  File "C:/python310/lib/weakref.py", line 46, in __getitem__
    o = self.data[key]()
KeyError: 'primary'

11.7. Tools for Working with Lists

Modul array menyediakan objek array() yang seperti daftar yang hanya menyimpan sebuah data dan menyimpannya dengan lebih ringkas.
 Contoh berikut menunjukkan larik angka yang disimpan untuk daftar reguler objek int Python:


>>> from array import array
>>> a = array('H', [4000, 10, 700, 22222])
>>> sum(a)
26932
>>> a[1:3]
array('H', [10, 700])

11.8. Decimal Floating Point Arithmetic

Modul desimal menawarkan tipe data Desimal untuk aritmatika titik mengambang desimal. Dibandingkan dengan implementasi float built-in dari floating point biner, kelas ini sangat membantu untuk

    aplikasi keuangan dan penggunaan lain yang memerlukan representasi desimal yang tepat,

    kontrol atas presisi,

    kontrol atas pembulatan untuk memenuhi persyaratan hukum atau peraturan,

    pelacakan tempat desimal yang signifikan, atau

    aplikasi di mana pengguna mengharapkan hasil yang sesuai dengan perhitungan yang dilakukan dengan tangan.

contoh :

>>> from decimal import *
>>> round(Decimal('0.70') * Decimal('1.05'), 2)
Decimal('0.74')
>>> round(.70 * 1.05, 2)
0.73
