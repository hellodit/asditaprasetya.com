---
title: Simple Guide to Understand Database Transaction
tags:
  - Database
  - Backend Engineering
categories: 
  - Software Architecture
date: 2020-10-25T08:43:26+07:00
draft: false
description: Cara mudah untuk memahami transaksi basis data
---

![](https://cdn-images-1.medium.com/max/800/1*sFQIBMdiDmLwcQbp3aOeow.jpeg)

Andi ingin mengirim uang ke Reni untuk dibelikan kopi kekinian menggunakan aplikasi dompet digital. Sedangkan, untuk mengirimkan uang diperlukan setidaknya 4 _query_ ke basis data dari awal sampai uang terkirim ke akun Reni.

Lantas, bagaimana jika di tengah jalan tiba-tiba proses terhenti karena terjadi kesalahan sistem? Bisa saja uang Andi sudah terpotong tetapi uang yang ada di rekening Rani belum bertambah. Hal ini dapat menimbulkan data yang tidak konsisten dan kerugian bagi pengguna aplikasi. Untuk mengatasinya, kita bisa menggunakan _Database Transaction._

### What is _database transaction?_

Dewasa ini hampir semua basis data baik SQL maupun NoSQL telah memiliki fitur untuk melakukan _database transaction._ Secara singkat _database transaction_ merupakan kemampuan basis data untuk menjamin bahwa semua proses yang sedang atau akan dijalankan memberikan nilai keberhasilan. Jika terjadi kesalahan pada salah satu proses, semua proses tersebut akan dibatalkan.

Untuk membantu dalam pemahaman mengenai _database transaction,_ dapat dilihat pada gambar berikut:

![](https://cdn-images-1.medium.com/max/800/1*VC4Vq1ZLVxFU_ZKNIEzOBg.png)

Dari jumlah _n-query_ yang dijalankan pada gambar, terdapat satu kesalahan pada _query 3_. Saat itulah semua proses yang telah berjalan akan dibatalkan dan dianggap tidak pernah terjadi oleh basis data.

![](https://cdn-images-1.medium.com/max/800/1*EEMZ4tYVYMEaAaYzAV36kw.png)

Dari jumlah _n-query_ yang akan dijalankan, semuanya berhasil dieksekusi dan semua perubahan data akan tersimpan dalam basis data.

> **Tujuan utama dari penggunaan _database transaction_ adalah untuk menjaga integritas data.**

### When to use database transaction?

_Database transaction_ dapat digunakan untuk membuat fitur yang melakukan lebih dari satu _query_ dalam satu eksekusi. Contohnya adalah fitur kirim uang. _Query_ yang dibutuhkan dari awal sampai selesai kurang lebih seperti ini:

1.  Memeriksa apakah uang yang akan dikirim lebih dari jumlah saldo
2.  Memeriksa tujuan apakah valid atau tidak
3.  Melakukan _update_ saldo pada pengirim
4.  Melakukan _update_ saldo pada penerima

![](https://cdn-images-1.medium.com/max/800/1*qLU0rJnTMDKFS3eiI2DZdw.png)

### _Technical concept_

Dalam _Database transaction_ setidaknya terdapat 3 tahapan yang perlu dipahami, yaitu:

#### **Begin**

Proses ini akan menjalankan semua _query_ yang telah ditentukan secara berurutan dari awal sampai akhir. Biasanya proses berlangsung secara _blocking_ atau _sync_.

#### **Commit**

Proses ini berjalan ketika semua _query_ telah dijalankan dan tidak terjadi kesalahan. Proses _commit_ menyimpan data dari hasil eksekusi.

![](https://cdn-images-1.medium.com/max/800/1*AX7GKU0GOqfKA50Gx5mo0g.png)

#### **Rollback**

Merupakan mekanisme yang dieksekusi jika terjadi kesalahan di salah satu _query_ yang dieksekusi. Jika terdapat satu saja kesalahan, semua _query_ akan dibatalkan dan data akan dikembalikan ke tahap sebelum proses _begin_.

![](https://cdn-images-1.medium.com/max/800/1*IP_IAATN7BpTjW8zn-Rs_Q.png)

### How to use?

Setiap basis data memiliki cara implementasi _Database transaction_ yang berbeda, tetapi secara umum proses yang ada adalah **begin, commit dan rollback.**

Beberapa _framework_ populer telah memiliki fitur _database transaction. S_alah satu yang sering saya gunakan adalah Laravel. untuk mengetahui bagaimana cara menerapkan _database transaction,_ dapat membaca di [Laravel Documentation](https://laravel.com/docs/8.x/database#database-transactions), atau dapat melihat _source code_ [mini-ewallet](https://github.com/hellodit/mini-ewallet) yang saya buat dengan menerapkan _database transaction._

### Summary

_Database transaction_ merupakan hal yang wajib diimplementasikan pada fitur yang memerlukan banyak proses _query_ dalam sekali eksekusi. Hal ini sebagai rancangan mitigasi ketika terjadi kesalahan di tengah proses yang sedang berlangsung serta untuk memastikan proses berjalan dengan benar.


Original post from [Tlab Circle](https://medium.com/@hellodit/database-transaction-97666f35bf87)  on June 11, 2021.