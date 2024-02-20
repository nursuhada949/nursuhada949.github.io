---
---
# Integrasi Mikrotik dengan FreeRadius
## Instalasi FreeRadius
![topologi11](https://github.com/nursuhada949/Lab-smk/assets/156059402/17ac0745-8cf1-4880-bf72-aae163228c77)

Pertama, kita akan melakukan instalasi FreeRadius. Kali ini kita akan menggunakan sebuah PC Server dengan sistem operasi Linux Ubuntu. Langkah instalasinya pun cukup mudah, kita tinggal ketikkan pada Terminal Linux sebuah command line seperti berikut:

## sudo apt-get install freeradius freeradius-utils freeradius-mysql
FreeRa![radiusd1](https://github.com/nursuhada949/Lab-smk/assets/156059402/07836165-0b1f-44d8-9564-9e0e183b9973)
dius ini bukanlah sebuah aplikasi besar sehingga untuk instalasinya sendiri tidak memerlukan begitu banyak space dari media penyimpanan. Nah, setelah proses instalasi selesai, kita akan melakukan sedikit penyesuain pada FreeRadius. Secara dasar kita akan melakukan konfigurasi pada file di FreeRadius, yaitu radiusd.conf, clients.conf, dan users.

## Integrasi Mikrotik dengan FreeRadius

Supaya FreeRadius dapat berintegrasi dengan Mikrotik, maka kita perlu melakukan konfiguasi pada masing-masing perangkat baik pada RADIUS Server (FreeRadius) dan juga RADIUS Client (Mikrotik). Kita akan mencoba melakukan konfigurasi seperti pada contoh topologi berikut. Kita akan membangun sebuah service hotspot dengan username dan password tersimpan pada FreeRadius.
Pertama, kita akan mengedit pada file radiusd.conf. Dengan menggunakan Terminal Linux ketikkan command line berikut:

## sudo nano /etc/freeradius/radiusd.conf
![client2](https://github.com/nursuhada949/Lab-smk/assets/156059402/bbfb957a-9ffe-4062-99bb-c91217b773eb)

Kemudian kita pastikan untuk line dengan script "$INCLUDE clients.conf" tidak terdapat tanda "#", yang artinya script tersebut telah aktif. Tetapi jika masih ada tanda "#" didepannya maka script tersebut belum aktif.
Selanjutanya kita akan konfigurasi pada file clients.conf. Dengan file ini kita akan menentukan perangkat RADIUS Client yang akan terkoneksi ke FreeRadius. Kita ketikkan sebuah command line pada Terminal linux seperti berikut.

## sudo nano /etc/freeradius/clients.conf

Pada file tersebut kita akan tambahkan sebuah scri!
pt yang berupa alamt IP Address dari RADIUS Client (Mikrotik) dan juga Secret yang akan digunakan oleh RADIUS Client terkoneksi ke FreeRadius. Kedua jenis parameter tersebut yang utama. Kita juga bisa menambahkan parameter yang lain namun hanya optional saja. Nah, seperti topologi diatas kita isikan IP Address dari Mikrotik yaitu 172.16.1.25 dan secret yaitu coba12345. Kita bisa menambahkan pada baris paling bawah dengan contoh format penulisan seperti tampilan berikut.
Langkah selanjutnya kita akan menambahakan akun berupa username dan password yang digunakan untuk login hotspot. Kita tambahkan kombinasi user dan password tersebut pada file Users. Kita ketikkan pada Terminal Linux sebuah command line seperti berikut.

## sudo nano /etc/freeradius/users

Kemudian kita tambahkan pada file tersebut sebuah script seperti pada tampilan dibawah ini. Kita akan mencoba menambhakan username=coba dan password=12345, dan yang kedua username=test dan password=test123
Nah, sampai dilangkah ini kita bisa melakukan pengetesan apakah konfigurasi pada FreeRadius berjalan dengan baik. Kita bisa menggunakan perintah seperti berikut:

## radtest coba 12345 localhost 1812 testing123

Pada format diatas kita mencoba salah satu username dan password yang telah kita buat, yaitu username=coba dan password=12345. Apabila berhasil maka akan muncul tampilan seperti gambar dibawah ini.
Jika terdapat keterangan Access-Accept maka Freeradius telah berjalan dengan baik namun jika terdapat keterangan Access-Reject maka hal itu menandakan terdapat setingan yang kurang tepat.

Kita juga bisa melakukan debug dengan menggunakan perintah freeradius -X. Nah, sampai sini konfigurasi freeradius sudah selesai.

## Konfigurasi Mikrotik

Setelah kita menyelesaikan setting FreeRadius, langkah selanjutnya kita akan melakukan konfigurasi disisi Router Mikrotik. Untuk konfigurasi hotspot pada mikrotik sendiri bisa kita lihat pada artikel sebelumnya disini.

Setelah service hotspot sudah kita tambahkan pada router mikrotik, kita akan melakukan integrasi supaya router bisa mengambil data username dan password login hotspot yang berada di RADIUS Server eksternal. Langkah-langkahnya cukup mudah. Pertama kita pilih menu Radius -> Klik Add [+], kemudian akan muncul tampilan seperti berikut.
Karena kita akan membuat service hotspot maka kita pilih pada paremeter 'Service' yaitu hotspot. Dan jangan lupa untuk menentukan IP Address dari perangkat RADIUS Server 172.16.1.100 dan juga secret untuk RADIUS Client seperti yang kita tambahkan pada aplikasi freeradius diatas, yaitu coba12345.

Selanjutnya pada menu hotspot, di bagian server profile kita tentukan juga untuk menggunakan data dari RADIUS Server.
Setelah semua langkah-langkah diatas sudah kita lakukan, maka kita akan mencoba untuk menggunakan service hotspot tersebut dengan username dan password yang terdapat pada database dari FreeRadius. Kita akan menggunakan salah satu akun yang telah kita buat sebelumnya, misal kita memakai username=test dan password=test123. Dan apabila kita sudah berhasil login, kita bisa monitoring perangkat client pada tab 'Active'.

Apabila kita lihat maka pada client tersebut terdapat sebuah tanda/flag 'R' (Radius) yang mengindikasikan bahwa client tersebut menggunakan akun dari RADIUS Server.
Nah, demikianlah bagaimana cara konfigurasi dasar untuk mengintegrasikan Mikrotik dengan FreeRadius. Untuk yang lebih advance lagi, sehingga kita bisa lebih mudah dari segi management user, kita bisa melakukan kombinasi dengan MySQL Server (sebagai penyimpanan database yang lebih fleksibel).
Dan juga bisa dikombinasi dengan aplikasi-aplikasi lain untuk management user seperti Access Manager, DaloRadius, phpRADmin, dll.




