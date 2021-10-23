## *Implementasi data kedalam MySQL*

berikut adalah bentuk penerapan perintah perintah dari DDL, DCL, DML, dan DQL berdasarkan ER diagram yang telah dibuat
Hal yang harus dilakukan adalah memilih software DBMS dan karean device telah terinstall Xampp maka 
telah ada paket MySQL juga, jadi tinggal dipakai secara terpisah

1. masuk sebagai root, dengan perintah
```bash
mysql -u root -p
Enter password:
```

2. setelah itu adalah membuat database serta membuat user baru selain root
```bash
MariaDB[(none)]> CREATE DATABASE film;
MariaDB[(none)]> USE film;
MariaDB[(none)]> CREATE USER 'mogar'@'localhost'IDENTIFIED BY'123';
```

3. memberikan izin atau hak akses pada database film
```bash
MariaDB[(none)]> GRANT ALL PRIVILEGES ON film.* TO 'mogar'@'localhost';
```

4. masuk sebagai user baru (mogar) dan membuat tabel 
```bash
MariaDB[(none)]> mysql -u mogar p;
Enter password: ***

MariaDB[(none)]>USE film;

MariaDB[(film)]>CREATE TABLE member (id_member INT AUTO_INCREMENT PRIMARY KEY, nama_member VARCHAR(50) NOT NULL, tipe_member VARCHAR(50) NOT NULL);

MariaDB[(film)]>CREATE TABLE theater (id_theater INT AUTO_INCREMENT PRIMARY KEY, nama_theater VARCHAR(50) NOT NULL, kota VARCHAR(50) NOT NULL);

MariaDB[(film)]>CREATE TABLE tipe_member (tipe_member VARCHAR(50) NOT NULL, keterangan_member VARCHAR(50) NOT NULL);

MariaDB[(film)]>CREATE TABLE movie (id_movie INT AUTO_INCREMENT PRIMARY KEY, nama_movie VARCHAR(50) NOT NULL);

MariaDB[(film)]>CREATE TABLE faktur (id_faktur INT AUTO_INCREMENT PRIMARY KEY, id_member INT, id_theater INT, id_movie INT, waktu_tayang VARCHAR(100) NOT NULL, harga_tiket INT(50), qty_tiket INT(50) NOT NULL, CONSTRAINT fk_member FOREIGN KEY (id_member) REFERENCES member(id_member), CONSTRAINT fk_theater FOREIGN KEY (id_theater) REFERENCES theater(id_theater), CONSTRAINT fk_movie FOREIGN KEY (id_movie) REFERENCES movie(id_movie));
```

5. menampilkan tabel dan atributnya
```bash
MariaDB [film]> DESCRIBE member;
+-------------+-------------+------+-----+---------+----------------+
| Field       | Type        | Null | Key | Default | Extra          |
+-------------+-------------+------+-----+---------+----------------+
| id_member   | int(11)     | NO   | PRI | NULL    | auto_increment |
| nama_member | varchar(50) | NO   |     | NULL    |                |
| tipe_member | varchar(50) | NO   |     | NULL    |                |
+-------------+-------------+------+-----+---------+----------------+
3 rows in set (0.131 sec)

MariaDB [film]> DESCRIBE tipe_member;
+-------------------+-------------+------+-----+---------+-------+
| Field             | Type        | Null | Key | Default | Extra |
+-------------------+-------------+------+-----+---------+-------+
| tipe_member       | varchar(50) | NO   |     | NULL    |       |
| keterangan_member | varchar(50) | NO   |     | NULL    |       |
+-------------------+-------------+------+-----+---------+-------+
2 rows in set (0.111 sec)

MariaDB [film]> DESCRIBE theater;
+--------------+-------------+------+-----+---------+----------------+
| Field        | Type        | Null | Key | Default | Extra          |
+--------------+-------------+------+-----+---------+----------------+
| id_theater   | int(11)     | NO   | PRI | NULL    | auto_increment |
| nama_theater | varchar(50) | NO   |     | NULL    |                |
| kota         | varchar(50) | NO   |     | NULL    |                |
+--------------+-------------+------+-----+---------+----------------+
3 rows in set (0.127 sec)

MariaDB [film]> DESCRIBE movie;
+------------+-------------+------+-----+---------+----------------+
| Field      | Type        | Null | Key | Default | Extra          |
+------------+-------------+------+-----+---------+----------------+
| id_movie   | int(11)     | NO   | PRI | NULL    | auto_increment |
| nama_movie | varchar(50) | NO   |     | NULL    |                |
+------------+-------------+------+-----+---------+----------------+
2 rows in set (0.086 sec)

MariaDB [film]> DESCRIBE faktur;
+--------------+--------------+------+-----+---------+----------------+
| Field        | Type         | Null | Key | Default | Extra          |
+--------------+--------------+------+-----+---------+----------------+
| id_faktur    | int(11)      | NO   | PRI | NULL    | auto_increment |
| id_member    | int(11)      | YES  | MUL | NULL    |                |
| id_theater   | int(11)      | YES  | MUL | NULL    |                |
| id_movie     | int(11)      | YES  | MUL | NULL    |                |
| waktu_tayang | varchar(100) | NO   |     | NULL    |                |
| harga_tiket  | int(50)      | YES  |     | NULL    |                |
| qty_tiket    | int(1)       | NO   |     | NULL    |                |
+--------------+--------------+------+-----+---------+----------------+
7 rows in set (0.081 sec)
```

6. insert data kedalam tabel
```bash
MariaDB [film]> INSERT INTO member (nama_member, tipe_member) VALUES('Muri','EPC'),('Luga','ELT'),('Rigo','MCT');

MariaDB [film]> INSERT INTO theater (nama_theater, kota) VALUES('Paris Van Java','Bandung'),('Grand Indonesia','Jakarta');

MariaDB [film]> INSERT INTO tipe_member(tipe_member, keterangan_member) VALUES('EPC','Epic'),('ELT','Elit'),('MCT','Mythic');

MariaDB [film]> INSERT INTO member (nama_member, tipe_member) VALUES('Muri','EPC'),('Luga','ELT'),('Rigo','MCT');

MariaDB [film]> INSERT INTO movie (nama_movie) VALUES('Orang Kaya Baru'),('Terlalu Tampan'),('Twice Land'),('Escape Room'), ('Welcome Home');

MariaDB [film]> INSERT INTO faktur (id_member, id_theater, id_movie, waktu_tayang, harga_tiket, qty_tiket) VALUES(1,1,1'22/01/2019 17:00',35000, 3), (1,2,3'22/01/2019 19:00',35000, 3), (2,2,3'22/01/2019 19:00',35000, 2), (2,2,4'22/01/2019 21:00',35000, 2), (3,1,1'22/01/2019 17:00',35000, 3), (1,2,2'22/01/2019 19:00',35000, 3), (3,1,5'22/01/2019 21:00',35000, 3), (2,2,2'22/01/2019 19:00',35000, 2);
```

7. menampilkan tabel yang telah diinsrt data
```bash
MariaDB [film]> SELECT * FROM member;
+-----------+-------------+-------------+
| id_member | nama_member | tipe_member |
+-----------+-------------+-------------+
|         1 | Muri        | EPC         |
|         2 | Luga        | ELT         |
|         3 | Rigo        | MCT         |
+-----------+-------------+-------------+
3 rows in set (0.174 sec)

MariaDB [film]> SELECT * FROM tipe_member;
+-------------+-------------------+
| tipe_member | keterangan_member |
+-------------+-------------------+
| EPC         | Epic              |
| ELT         | Elit              |
| MCT         | Mythic            |
+-------------+-------------------+
3 rows in set (0.001 sec)

MariaDB [film]> SELECT * FROM theater;
+------------+-----------------+---------+
| id_theater | nama_theater    | kota    |
+------------+-----------------+---------+
|          1 | Paris Van Java  | Bandung |
|          2 | Grand Indonesia | Jakarta |
+------------+-----------------+---------+
2 rows in set (0.001 sec)

MariaDB [film]> SELECT * FROM movie;
+----------+-----------------+
| id_movie | nama_movie      |
+----------+-----------------+
|        1 | Orang Kaya Baru |
|        2 | Terlalu Tampan  |
|        3 | Twice Land      |
|        4 | Escape Room     |
|        5 | Welcome Home    |
+----------+-----------------+
5 rows in set (0.001 sec)

MariaDB [film]> SELECT * FROM faktur;
+-----------+-----------+------------+----------+------------------+-------------+-----------+
| id_faktur | id_member | id_theater | id_movie | waktu_tayang     | harga_tiket | qty_tiket |
+-----------+-----------+------------+----------+------------------+-------------+-----------+
|        17 |         1 |          1 |        1 | 22/01/2019 17:00 |       35000 |         3 |
|        18 |         1 |          2 |        3 | 22/01/2019 19:00 |       35000 |         3 |
|        19 |         2 |          2 |        3 | 22/01/2019 19:00 |       35000 |         2 |
|        20 |         2 |          2 |        4 | 22/01/2019 21:00 |       35000 |         2 |
|        21 |         3 |          1 |        1 | 22/01/2019 17:00 |       35000 |         3 |
|        22 |         1 |          2 |        2 | 22/01/2019 19:00 |       35000 |         3 |
|        23 |         3 |          1 |        5 | 22/01/2019 21:00 |       35000 |         3 |
|        24 |         2 |          2 |        2 | 22/01/2019 19:00 |       35000 |         2 |
+-----------+-----------+------------+----------+------------------+-------------+-----------+
8 rows in set (0.001 sec)
```