# Modul2_C09
Kelompok C09
- 05111840000028  M. Frediansyah Sinaga
- 05111840000072  Kresna Adhi Pramana

Praktikum Modul 2 berupa *UML, DNS (Domain Name System), dan Web Server*.


## Soal
![Soal 1](img/soal1.PNG)
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
      1. Install bind9 di MALANG
      2. Isikan configurasi http://semeruc09.pw di named.conf.local
      ![Foto 1](img/1.PNG)
      3. Buat folder jarkom di dalam /etc/bind
      4. Copykan file db.local pada path /etc/bind ke dalam folder jarkom yang baru saja dibuat dan ubah namanya menjadi semeruc09.pw
      5. Kemudian buka file semeruc09.pw dan edit seperti gambar berikut
      ![Foto 2](img/2.PNG)
      6. Restart bind9
      7. Test dengan mengubah nameserver di GRESIK dan ping semeruc09.pw
      ![Foto 3](img/3.PNG)
      
   2. Membuat alias http://www.semeruc09.pw
      1. Buka file semeruc09.pw pada server MALANG dan tambahkan konfigurasi seperti pada gambar berikut: 
      ![Foto a](img/a.PNG)
      2. Restart bind9
      3. Untuk test, bisa ping www.semeruc09.pw di GRESIK
      ![Foto 4](img/4.PNG)
      
   3. Buat subdomain http://penanjakan.semeruc09.pw 
      1. Edit file /etc/bind/jarkom/semeruc09.pw lalu tambahkan subdomain untuk semeruc09.pw yang mengarah ke IP PROBOLINGGO. 
      ![Foto 5](img/5.PNG)
      2. Restart service bind
      3. Test ping penanjakan.semeru.c09.pw
      ![Foto 6](img/6.PNG)
      
   4. Reverse domain untuk domain utama
      1. Edit file /etc/bind/named.conf.local pada MALANG 
      2. Tambahkan konfigurasi berikut
      ![Foto 7](img/7.PNG)
      3. Copykan file db.local pada path /etc/bind ke dalam folder jarkom yang baru saja dibuat.
      4. Edit file 77.151.10.in-addr.arpa menjadi seperti gambar di bawah ini
      ![Foto 8](img/8.PNG)
      5. Kemudian restart bind9 
      6. Testing menggunakan host -t PTR 10.151.77.84 di GRESIK 
      ![Foto 9](img/9.PNG)
      
   5. Membuat DNS Server Slave pada MOJOKERTO
      1. Konfigurasi Pada Server MALANG
         1. Edit file /etc/bind/named.conf.local  
         ![Foto 10](img/10.PNG)
         2. Lakukan restart bind9
      2. Konfigurasi Pada Server MOJOKERTO
         1. Buka file /etc/bind/named.conf.local pada MOJOKERTO dan tambahkan syntax berikut:
         ![Foto 11](img/11.PNG)
         2. Lakukan restart bind9
      3. Testing
         1. Pada server MALANG matikan service bind9
         2. Pada client GRESIK pastikan pengaturan nameserver mengarah ke IP MALANG dan IP MOJOKERTO
         3. Lakukan ping ke semeruc09.pw pada client GRESIK.
         ![Foto 12](img/12.PNG)
        
   6. Buat subdomain dengan alamat http://gunung.semeruc09.pw yang didelegasikan pada server MOJOKERTO dan mengarah ke IP Server PROBOLINGGO. 
      1. Konfigurasi Pada Server MALANG
         1. Pada MALANG, edit file /etc/bind/jarkom/semeruc09.pw dan ubah menjadi seperti di bawah ini
         ![Foto 13](img/13.PNG)
         2. Kemudian edit file /etc/bind/named.conf.options pada MALANG.
         3. Kemudian comment dnssec-validation auto; dan tambahkan baris berikut pada /etc/bind/named.conf.options : `allow-query{any;};`
         ![Foto 14](img/14.PNG)
         4. Kemudian edit file /etc/bind/named.conf.local menjadi seperti gambar di bawah:
         ![Foto 15](img/15.PNG)
         5. Setelah itu restart bind9
      2. Konfigurasi Pada Server MOJOKERTO
         1. Pada MOJOKERTO edit file /etc/bind/named.conf.options
         2. Kemudian comment dnssec-validation auto; dan tambahkan baris berikut pada /etc/bind/named.conf.options `Allow-query{any;};` 
         ![Foto 16](img/16.PNG)
         3. Lalu edit file /etc/bind/named.conf.local
         ![Foto 17](img/17.PNG)
         4. Kemudian buat direktori dengan nama delegasi
         5. Copy db.local ke direktori pucang dan edit namanya menjadi gunung.semeruc09.pw
         6. Kemudian edit file gunung.semeruc09.pw
         ![Foto 18](img/18.PNG)
         7. Restart bind9
      3. Testing
         1. Lakukan ping ke domain gunung.semeruc09.pw dari GRESIK
         ![Foto 19](img/19.PNG)
         

   7. Buat subdomain dengan nama http://naik.gunung.semeruc09.pw, domain ini diarahkan ke IP Server PROBOLINGGO.
      1. Edit file gunung.semeruc09.pw di MOJOKERTO
      ![Foto 20](img/20.PNG)
      2. Kemudian Restart bind9
      3. Testing di GRESIK
      ![Foto 21](img/21.PNG)
     
      
   8. Domain http://semeruyyy.pw memiliki DocumentRoot pada /var/www/semeruyyy.pw.
      1. Install apache2 di PROBOLINGGO
      2. Install php
      3. Download file dengan wget di /var/www/
      4. Lalu setting di /etc/apache2/sites-available/semeruc09.pw.conf
      ![Foto 22](img/22.PNG)
      5. Jalankan a2ensite, lalu Reload dan restart apache2
      6. Testing :
      ![Foto 23](img/23.PNG)
      

   9. Aktifkan mod rewrite agar urlnya menjadi http://semeruyyy.pw/home. (Referensi jawaban :https://stackoverflow.com/questions/14149339/htaccess-short-url)
      1. Jalankan perintah a2enmod rewrite untuk mengaktifkan module rewrite. Lalu restart apache2.
      2. Buat file .htaccess di /var/www/semeruc09.pw dan diisi dengan :
      ![Foto 24](img/24.PNG)
      3. Edit file semeruc09.pw.conf
      ![Foto 25](img/25.PNG)
      4. Restart apache
      5. Testing, buka  http://semeruyyy.pw/home.
      ![Foto 26](img/26.PNG)
      

   10. Web http://penanjakan.semeruc09.pw akan digunakan untuk menyimpan assets file yang memiliki DocumentRoot pada /var/www/penanjakan.semeruc09.pw 
        dan memiliki struktur folder sebagai berikut:
       ![Foto 27](img/27.PNG)
       1. setting di /etc/apache2/sites-available/penanjakan.semeruc09.pw.conf
       ![Foto 28](img/28.jpg)
       2. Jalankan a2ensite, lalu Reload dan restart apache2
       ![Foto 29](img/29.jpg)

   11. Pada folder /public dibolehkan directory listing namun untuk folder yang berada di dalamnya tidak dibolehkan.
       1. Pindah ke directory /etc/apache2/sites-available kemudian buka file penanjakan.semeruc09.pw.conf , lalu tambahkan   
       ![Foto 30](img/30.jpg)
       2. Restart apache
       3. Testing
       ![Foto 31](img/31.jpg)
       ![Foto 32](img/32.jpg)
       ![Foto 33](img/33.jpg)
       ![Foto 34](img/34.jpg)

   12. Untuk mengatasi HTTP Error code 404, disediakan file 404.html pada folder /errors untuk mengganti error default 404 dari Apache.
       1. Menambahkan ErrorDocument 404 /errors/404.html di file penanjakan.semeruc09.pw.conf
       ![Foto 35](img/35.jpg)
       2. Testing
       ![Foto 36](img/36.jpg)
       
   13. Untuk mengakses file assets javascript awalnya harus menggunakan url http://penanjakan.semeruc09.pw/public/javascripts. Karena terlalu panjang maka dibuatkan konfigurasi
        virtual host agar ketika mengakses file assets menjadi http://penanjakan.semeruc09.pw/js.
       1. Edit file penanjakan.semeruc09.pw.conf ditambah Alias
       ![Foto 37](img/37.jpg)
       2. Testing
       ![Foto 38](img/38.jpg)
       
   14. Web http://naik.gunung.semeruc09.pw sudah bisa diakses hanya dengan menggunakan port 8888. DocumentRoot web berada pada /var/www/naik.gunung.semeruc09.pw.
       1. Download file naik.gunung.semeruc09.pw dengan wget
       2. Edit file naik.gunung.semeruc09.pw dengan VirtualHost = 8888 dan Documentroot nya sesuaikan 
       ![Foto 38](img/38.jpg)
       3. Tambahkan port 8888 pada file ports.conf
       ![Foto 40](img/40.jpg)
       4. Jalankan a2ensite lalu reload dan restart
       5. Testing
       ![Foto 41](img/41.jpg)

   15. Buat web http://naik.gunung.semeruyyy.pw agar diberi autentikasi password dengan username “semeru” dan password “kuynaikgunung” supaya aman dan tidak sembarang orang 
        bisa mengaksesnya. (referensi jawaban : https://www.digitalocean.com/community/tutorials/how-to-set-up-password-authentication-with-apache-on-ubuntu-14-04)
       1. Buat File passwordnya dengan command htpasswd -c /etc/apache2/.htpasswd semeru
       2. Lalu akan keluar password yang mau diisi, isi dengan kuynaikgunung, setelah itu password akan disimpan secara terenkripsi
       ![Foto 42](img/42.jpg)
       3. Lalu, pada file naik.gunung.semeruc09.pw.conf ditambahkan :
            ```
            <Directory "/var/www/html">
               AuthType Basic
               AuthName "Restricted Content"
               AuthUserFile /etc/apache2/.htpasswd
               Require valid-user
             </Directory>
             ```
       ![Foto 43](img/43.jpg)
       4. Restart apache
       5. Testing
       ![Foto 44](img/44.jpg)
       ![Foto 45](img/45.jpg)
       ![Foto 46](img/46.jpg)

   16.  Setiap mengunjungi IP PROBOLINGGO akan dialihkan secara otomatis ke http://semeruc09.pw. (referensi jawaban : https://www.digitalocean.com/community/questions/redirect-
         ip-address-to-domain-name-apache)
        1. Dengan cara, membuat direktori bernama alihkan di /var/www/ , lalu mengedit file 000-default yang DocumentRootnya diarahkan ke /var/www/alihkan dan edit agar dapat 
          membaca .htaccess
        ![Foto 47](img/47.jpg)
        2. Lalu, buat file .htaccess di dalam folder alihkan, yg berisi :
        ![Foto 48](img/48.jpg)
        3. Restart apache
        4. Testing
           1. Sebelum 
           ![Foto 49](img/49.jpg)
           2. Sesudah
           ![Foto 50](img/50.jpg)

   17. Karena pengunjung pada /var/www/penanjakan.semeruc09.pw/public/images sangat banyak maka semua request gambar yang memiliki substring “semeru” akan diarahkan menuju 
        semeru.jpg.(referensi jawaban : https://www.mynotepaper.com/how-to-redirect-url-using-htaccess-if-contains-specific-word)
       1. Edit file /etc/apache2/sites-available/penanjakan.semeruc09.pw.conf untuk bisa membaca .htaccess
       ![Foto 51](img/51.jpg)
       2. Tambahkan file .htaccess ke DocumentRoot penanjakan.semeruc09.pw 
       ![Foto 52](img/52.jpg)
       3. Testing, jika mengetik bukansemeruaja.jpg, tetap akan teralihkan ke semeru.jpg
       ![Foto 53](img/53.jpg)
       ![Foto 54](img/54.jpg)
       
