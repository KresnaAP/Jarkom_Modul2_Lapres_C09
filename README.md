# Modul2_C09
Kelompok C09
- 05111840000028  M. Frediansyah Sinaga
- 05111840000072  Kresna Adhi Pramana

Praktikum Modul 2 berupa *UML, DNS (Domain Name System), dan Web Server*.

## Soal
Semeru adalah salah satu gunung yang terkenal di Jawa Timur. Bibah adalah salah satu juru kunci
Semeru. Bibah ingin menyebarkan keindahan Semeru pada dunia sehingga dia membeli 3 buah server
yang berada di MALANG , MOJOKERTO dan PROBOLINGGO . Server MALANG akan digunakan
sebagai DNS Server Master, MOJOKERTO akan digunakan sebagai DNS Server Slave dan
PROBOLINGGO akan digunakan sebagai Web Server. Selain 3 server terdapat 2 klien yang digunakan
untuk testing oleh Bibah yaitu GRESIK dan SIDOARJO . Untuk menyambungkan semua jaringan
tersebut Bibah memberi router di SURABAYA .

Kalian diminta untuk membuat sebuah website utama dengan (1) alamat http://semeruyyy.pw yang
memiliki (2) alias http://www.semeruyyy.pw , dan (3) subdomain
http://www.penanjakan.semeruyyy.pw yang diatur DNS-nya pada MALANG dan mengarah ke IP
Server PROBOLINGGO serta dibuatkan (4) reverse domain untuk domain utama. Untuk mengantisipasi
server dicuri/rusak, Bibah minta dibuatkan (5) DNS Server Slave pada MOJOKERTO agar Bibah tidak
terganggu menikmati keindahan Semeru pada Website. Selain website utama Bibah juga meminta
dibuatkan (6) subdomain dengan alamat http://gunung.semeruyyy.pw yang didelegasikan pada server
MOJOKERTO dan mengarah ke IP Server PROBOLINGGO . Bibah juga ingin memberi petunjuk
mendaki gunung semeru kepada anggota komunitas sehingga dia meminta dibuatkan (7) subdomain
dengan nama http://naik.gunung.semeruyyy.pw , domain ini diarahkan ke IP Server PROBOLINGGO.

Setelah selesai membuat keseluruhan domain, kamu diminta untuk segera mengatur web server. (8)
Domain http://semeruyyy.pw memiliki DocumentRoot pada /var/www/semeruyyy.pw . Awalnya web
dapat diakses menggunakan alamat http:// semeruyyy.pw /index.php/home . Karena dirasa alamat urlnya
kurang bagus, maka (9) diaktifkan mod rewrite agar urlnya menjadi http:// semeruyyy.pw /home .
(10) Web http://penanjakan.semeruyyy.pw akan digunakan untuk menyimpan assets file yang
memiliki DocumentRoot pada /var/www/ penanjakan.semeruyyy.pw dan memiliki struktur
folder sebagai berikut:
/var/www/ penanjakan.semeruyyy.pw
/public/javascripts
/public/css
/public/images
/errors

(11) Pada folder /public dibolehkan directory listing namun untuk folder yang berada di dalamnya
tidak dibolehkan. (12) Untuk mengatasi HTTP Error code 404, disediakan file 404.html pada
folder /errors untuk mengganti error default 404 dari Apache. (13) Untuk mengakses file assets
javascript awalnya harus menggunakan url http:// penanjakan.semeruyyy.pw /public/javascripts .
Karena terlalu panjang maka dibuatkan konfigurasi virtual host agar ketika mengakses file assets
menjadi http:// penanjakan.semeruyyy.pw /js .
Untuk web http:// gunung.semeruyyy.pw belum dapat dikonfigurasi pada web server karena
menunggu pengerjaan website selesai. (14) sedangkan web http:// naik.gunung.semeruyyy.pw
sudah bisa diakses hanya dengan menggunakan port 8888. DocumentRoot web berada pada
/var/www/ naik.gunung.semeruyyy.pw . Dikarenakan web http:// naik.gunung.semeruyyy.pw
bersifat private (15) Bibah meminta kamu membuat web http:// naik.gunung.semeruyyy.pw agar
diberi autentikasi password dengan username “ semeru ” dan password “ kuynaikgunung ” supaya
aman dan tidak sembarang orang bisa mengaksesnya.
Saat Bibah mengunjungi IP PROBOLINGGO , yang muncul bukan web utama
http:// semeruyyy.pw melainkan laman default Apache yang bertuliskan “It works!”. (16) Karena
dirasa kurang profesional, maka setiap Bibah mengunjungi IP PROBOLINGGO akan dialihkan
secara otomatis ke http:// semeruyyy.pw. (17) Karena pengunjung pada
/var/www/ penanjakan.semeruyyy.pw/public/images sangat banyak maka semua request gambar
yang memiliki substring “semeru” akan diarahkan menuju semeru.jpg.

## Jawaban
   1. Setting alamat utama : http://semeruc09.pw
      a. Install bind9 di MALANG
      b. Isikan configurasi http://semeruc09.pw di named.conf.local
      ![Foto 1](img/1.PNG)
      c. Buat folder jarkom di dalam /etc/bind
      d. Copykan file db.local pada path /etc/bind ke dalam folder jarkom yang baru saja dibuat dan ubah namanya menjadi semeruc09.pw
      e. Kemudian buka file semeruc09.pw dan edit seperti gambar berikut
      ![Foto 2](img/2.PNG)
      f. Restart bind9
      g. Test dengan mengubah nameserver di GRESIK dan ping semeruc09.pw
      ![Foto 3](img/3.PNG)
   2. Membuat alias http://www.semeruc09.pw
      a. Buka file semeruc09.pw pada server MALANG dan tambahkan konfigurasi seperti pada gambar berikut:
      ![Foto 4](img/4.PNG)
      b. Restart bind9
      c. Untuk test, bisa ping www.semeruc09.pw di GRESIK
      ![Foto 5](img/5.PNG)
   3. Buat subdomain http://penanjakan.semeruc09.pw 
      a. Edit file /etc/bind/jarkom/semeruc09.pw lalu tambahkan subdomain untuk semeruc09.pw yang mengarah ke IP PROBOLINGGO.
      ![Foto 6](img/6.PNG)
      b. Restart service bind
      c. Test ping penanjakan.semeru.c09.pw
      ![Foto 7](img/7.PNG)
   4. Reverse domain untuk domain utama
      a. Edit file /etc/bind/named.conf.local pada MALANG 
      b. Tambahkan konfigurasi berikut
      ![Foto 8](img/8.PNG)
      c. Copykan file db.local pada path /etc/bind ke dalam folder jarkom yang baru saja dibuat.
      d. Edit file 77.151.10.in-addr.arpa menjadi seperti gambar di bawah ini
      ![Foto 9](img/9.PNG)
      e. Kemudian restart bind9 
      f. Testing menggunakan host -t PTR 10.151.77.84 di GRESIK
      ![Foto 10](img/10.PNG)
   5. Membuat DNS Server Slave pada MOJOKERTO
      a. Konfigurasi Pada Server MALANG
          i. Edit file /etc/bind/named.conf.local
          ![Foto 11](img/11.PNG)
         ii. Lakukan restart bind9
      b. Konfigurasi Pada Server MOJOKERTO
          i. Buka file /etc/bind/named.conf.local pada MOJOKERTO dan tambahkan syntax berikut:
          ![Foto 12](img/12.PNG)
         ii. Lakukan restart bind9
      c. Testing
          i. Pada server MALANG matikan service bind9
         ii. Pada client GRESIK pastikan pengaturan nameserver mengarah ke IP MALANG dan IP MOJOKERTO
        iii. Lakukan ping ke semeruc09.pw pada client GRESIK.
        ![Foto 13](img/13.PNG)
   6. Buat subdomain dengan alamat http://gunung.semeruc09.pw yang didelegasikan pada server MOJOKERTO dan mengarah ke IP Server PROBOLINGGO. 
      a. Konfigurasi Pada Server MALANG
          i. Pada MALANG, edit file /etc/bind/jarkom/semeruc09.pw dan ubah menjadi seperti di bawah ini
          ![Foto 14](img/14.PNG)
         ii. Kemudian edit file /etc/bind/named.conf.options pada MALANG.
        iii. Kemudian comment dnssec-validation auto; dan tambahkan baris berikut pada /etc/bind/named.conf.options : `allow-query{any;};`
          ![Foto 15](img/15.PNG)
         iv. Kemudian edit file /etc/bind/named.conf.local menjadi seperti gambar di bawah:
          ![Foto 16](img/16.PNG)
          v. Setelah itu restart bind9


              















