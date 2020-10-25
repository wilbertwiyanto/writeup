<html>
<head>
<title> Blunder | Writeup
</title>
</head>
<body>
<div markdown="1">

# **BLUNDER WRITEUP**



## **ENUMERATION**

nmap untuk mencari open ports

![](/assets/messageImage_1603477004000.jpg)

lakukan gobuster untuk mencari directory

![](/assets/messageImage_1603477059821.jpg)

ketemu directory /admin dan ada login page

![](/assets/messageImage_1603477109679.jpg)

coba mencari-cari usernya

lalu pada gobuster ketemu /todo.txt dan mendapatkan potential usernya fergus

![](/assets/messageImage_1603477130409.jpg)

pada about, terdapat hint kalau pembuat web ini menyimpan seluruh fakta di web ini

![](/assets/messageImage_1603477152414.jpg)

gunakan tool cewl untuk membuat wordlist dari fakta-fakta pada web ini

![](/assets/messageImage_1603477236975.jpg)

![](/assets/messageImage_1603477270792.jpg)

gunakan burp untuk melakukan bruteforce login page yang ditemukan

![](/assets/messageImage_1603477473455.jpg)

![](/assets/messageImage_1603477496658.jpg)

![](/assets/messageImage_1603477520281.jpg)

ketemu credential fergus:RolandDeschain

gunakan credential tersebut untuk login ke /admin

Asumsi saya, bludit memiliki validasi seperti berikut untuk file upload:

- Pertama, memvalidasi apakah file tersebut memiliki extension php secara client side, jika iya maka akan ditolak langsung.

- Kedua, pada saat file sudah terkirim dari client side ke server side, server side memvalidasi jika file yang diupload memiliki extension png, maka akan dimasukkan ke dalam directory uploads/pages. Jika file tersebut memiliki extension php, maka akan dimasukan ke dalam directory tmp

[https://github.com/bludit/bludit/issues/1079](https://github.com/bludit/bludit/issues/1079)

membuat file php-reverse-shell.png lalu gunakan burp untuk merubah extension menjadi php

membuat file htaccess.png lalu gunakan burp untuk merubah nama file menjadi .htaccess

akses file php-reverse-shell.php pada directory /bl-content/tmp/php-reverse-shell.php

## **USER FLAG**

pada directory /var/www terdapat versi bludit yang lain yaitu versi 3.10.0a

lakukan enumerating dengan command

ketemu user baru dengan credential hugo:Password120

switch user hugo denga ncommand su hugo

ambil user.txt

## **ROOT FLAG**

gunakan sudo -l

user bisa melakukan (ALL, !root) /bin/bash [https://www.exploit-db.com/exploits/47502](https://www.exploit-db.com/exploits/47502)

gunakan command sudo -u#-1 /bin/bash

ambil root.txt

[back](https://wilbertwiyanto.github.io/website/)
</div>
</body>
</html>