# Tugas2-BigData Hadoop Ecosystem




Setelah melakukan Crawling data, kita akan mengimport data melalui ekosistem hadoop yaitu dengan Apache Sqoop. sebelumnya kita bisa pull mysql dan phpmyadmin dari docker hub
## Pull Mysql dan PHPMyadmin dari docker hub
Buka terminal atau command prompt dan jalankan perintah berikut untuk mengunduh image mysql danPHPMyadmin dari Docker Hub:
```
docker pull mysql 
docker pull phpmyadmin
```
## Mengkoneksikan Mysql dan PHPMyadmin ke container
Setelah mengunduh image Mysql dan PHPMyadmin dari Docker Hub, kita dapat jalankan container Mysql terlebih dahulu:
```
docker run --name mysql_db -e MYSQL_ROOT_PASSWORD=000 -d mysql:latest
```
--name adalah nama container dari Mysql
MYSQL_ROOT_PASSWORD=000 adalah password untuk Mysqlnya.

mysql:latest adalah versi dari Mysqlnya.

Setelah itu kita dapat jalankan container PHPMyadmin:
```
docker run --name phpmyadmin_db -d --link mysql_db:db -p 8081:80 phpmyadmin:latest
```
--name adalah nama container dari Mysql

--link mysql_db:db adalah menghubungkan database kita dengan container Mysql yang sebelumnya sudah dibuat

-p 8081:80 adalah membuka port 8081 dan membinding ke port 80 

phpmyadmin:latest adalah versi dari PHPMyadmin

Setelah itu kita dapat mengimport output dari crawling data ke localhost:8081

## Melakukan import dengan Apache Sqoop
Buka terminal atau command prompt dan jalankan perintah berikut untuk mengunduh image Apache Sqoop dari Docker Hub:
```
docker pull dvoros/sqoop
```
Setelah mengunduh image Apache Sqoop, kita akan menjalankan container Apache Sqoop:
```
docker run -v /path/to/jdbc-jars:/jdbc -it dvoros/sqoop:latest
```
Setelah dijalankan kita akan menuliskan perintah untuk mengimport data yang sudah diproses sebelumnya:
```
sqoop import --connect jdbc:mysql://localhost:8081/reviews --username root --password 000 --table reviews --target-dir /Users/aqila
```
//localhost:8081/reviews adalah URL koneksi ke basis data MySQL yang sudah dibuat sebelumnya
--username root adalah nama pengguna (username) yang digunakan untuk mengakses basis data MySQL

--password 000 adalah kata sandi (password) yang digunakan untuk mengakses basis data MySQL

--table reviews adalah nama tabel di basis data MySQL yang akan diimpor ke HDFS

--target-dir /Users/aqil adalah direktori target di HDFS di mana data yang diimpor akan disimpan



