# Dasar-Dasar SQL

Structured Query Language (SQL) adalah bahasa database standar yang digunakan dalam operasi basis data relasional. Baik itu untuk membuat, memelihara, dan serta melakukan operasi dasar seperti CRUD (create, retrieve, update, delete) hingga operasi kompleks yang melibatkan manipulasi data serta operasi aritmatika pada basis data relasional. Beberapa contoh basis data relasional yang umum digunakan adalah MySQL, PostgreSQL, dan SQL Server.

Beberapa hal yang perlu diketahui dalam penggunaan SQL adalah SQL tidak case sensitive, artinya penulisan perintah-perintah pada SQL tidak terpengaruh oleh huruf kecil ataupun huruf besar. Namun disarankan mengkapitalkan kata-kata kunci seperti SELECT, UPDATE, DELETE dst. Untuk pembuatan tabel dan kolom, juga disarankan untuk menggunakan huruf kecil.

Saat menjalankan beberapa perintah SQL atau umumnya disebut query ada kalanya kita ingin mendisable atau tidak menjalankan baris/query tertentu, hal yang dilakukan adalah dengan menambahkan tanda hubung ganda (--) di awal baris. Hal ini ekivalen dengan garis miring ganda (//) untuk tidak mengeksekusi baris tertentu pada beberapa bahasa pemrograman, misalnya PHP.

Meskipun ada standar [ISO](<https://en.wikipedia.org/wiki/ISO/IEC_9075>) untuk penulisan SQL, namun pada implementasinya ada sedikit perbedaan dalam sintaks masing-masing basis data relasional. Jadi ada beberapa kemungkinan dimana ada sintaks yang berfungis di SQL Server tapi tidak berfungsi jika dijalankan di MySQL, begitupun sebaliknya.

### Primary Key
Silahkan ditambahkan

### Foreign Key
Silahkan ditambahkan

### Collation
Silahkan ditambahkan

## Tipe Data
Silahkan ditambahkan

## Sintaks Dasar SQL
Beberapa perintah dasar dalam SQL meliputi perintah-perintah yang diperlukan dalam operasi dalam membuat dan menghapus database dan tabel di dalamnya, serta membuat, mengambil, memperbaharui dan memghapus data tertentu pada database.

### Membuat Database
```sql
CREATE DATABASE nama_database;
```

### Menghapus Database
```sql
DROP DATABASE nama_database;
```

### Membuat Tabel
```sql
CREATE TABLE nama_tabel (kolom1 tipe_data(ukuran), column2 tipe_data(ukuran), column3 tipe_data(ukuran));
```

### Menghapus Tabel
```sql
DROP TABLE nama_tabel;
```

### Mengosongkan Tabel
```sql
TRUNCATE TABLE nama_tabel;
```

> **Silahkan tambahkan catatan tambahan apa perbedaan antara perintah `DROP` dan perintah `TRUNCATE`**

## Operator

**tunggu untuk langkah selanjutnya ... 😃**
