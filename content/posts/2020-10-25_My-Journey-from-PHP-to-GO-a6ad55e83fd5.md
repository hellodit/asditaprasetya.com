---
title: My Journey from PHP to GO
tags:
  - GO Lang
categories: 
  - Self Documentation
date: 2020-10-25T08:43:26+07:00
draft: false
description: Belajar bahasa pemrograman baru tidaklah sulit jika sudah menguasai satu bahasa pemrograman.
---


Belajar bahasa pemrograman baru tidaklah sulit jika sudah menguasai satu bahasa pemrograman, karena pada dasarnya semua bahasa premrograman tidak memiliki perberdaan, mulai dari operator matematika, logika, fungsi, visibilitas, dll.

![](https://cdn-images-1.medium.com/max/800/0*hgW651RtC8sw55No)

### My programming background

Bagi saya PHP adalah bahasa ibu, PHP merupakan bahasa pemrograman pertama yang saya pelajari, terhitung sudah lebih dari 4 tahun saya menggunakan PHP dalam pengerjaan proyek profesional dan riset. PHP dikenal sebagai bahasa dengan tipe Dynamic typing. Dynamic typing artinya tidak diperlukan deklarasi tipe data dalam pembuatan variabel ataupun fungsi, sehingga memberikan kebebasan dan waktu yang ringkas untuk menulis kode saat mengembangakan perangkat lunak.

Sekitar 2 tahun belakangan saya mulai menggunakan Laravel dalam mengerjakan proyek, dengan menggunakan Laravel saya merasa sangat terbantu dengan berbagai fitur yang ada didalamnya, salah satunya adalah Object Relation Map (ORM) Eloquent dan blade templating.

Dari PHP murni sampai dengan menggunakan _Framework_ Laravel saya belajar sangat banyak mengenai cara menulis kode, mulai dari yang paling sederhana adalah arsitektur _model, view, controller_ (MVC), Design pattern, Object Oriented Programming (OOP), teknik pengembangan RESTFULL API, _Queue_ dan masih banyak lagi.

### Start learning Go

Setelah sekian lama berkarir dengan PHP akhirnya saya memutuskan untuk mempelajari bahasa pemrograman baru, dari beberapa bahasa yang sudah pernah saya pelajari sekilas (NodeJS, Python, Ruby dan Java) akhirnya saya memutuskan untuk memilih GO sebagai bahasa ke dua saya.

Go merupakan bahasa pemrograman yang dibuat di Google pada tahun 2009, untuk ukuran bahasa pemrograman Go (versi terakhir 1.15) masih sangatlah muda dibandingan dengan PHP yang dibuat pada tahun 1995 (versi terakhir 7.4.8), dari versi rilis public saja sudah terlihat jauh.

Terhitung bulan ke 4 saya belajar bahasa Go, sebagai _developer_ yang memiliki pengalaman di bahasa pemrograman PHP tidaklah mudah dan juga tidak susah untuk belajar GO, menurut saya belajar GO memiliki tantangan dan keseruan tersendiri.

Setelah 4 bulan saya memperdalam bahasa GO ada beberapa catatan yang saya buat dan akan saya bagikan, sebenarnya catatan ini adalah dokumentasi pribadi (jadi bisa saja salah), saya membagikan catatan pribadi ini dengan harapan adanya catatan ini akan membantu teman — teman yang memiliki background PHP dan ingin untuk belajar GO. Catatan ini **tidak untuk membandingkan antara GO dan PHP mana yang paling baik**, karena tiap bahasa pemrograman hanyalah sebuah alat, yang terpenting adalah bagaimana sebagai _developer_ mampu untuk memaksimalkan bahasa pemrograman.

### The notes
Berikut ini adalah catatan pribadi yang saya buat, jika ada kesalahan di mohon untuk memberikan koreksi dengan menghubungi media sosial atau meninggalkan komentar di postingan ini, terimakasih.

#### Static typing & Dynamic typing
PHP termasuk dalam tipe Dynamic typing, artinya tidak perlu untuk melakukan deklarasi tipe data saat pertama membuat variabel maupun fungsi, selain itu tipe data pada tiap variabel dapat digantikan dengan tipe data lain, contohnya variabel A memiliki nilai dengan tipe data string, selanjutnya variabel A di assign nilai dengan tipe data integer, hal ini tidak akan menimbulkan error.

Go memiliki termasuk tipe static typing yang artinya berkebalikan dengan dynamic typing. ketika membuat variabel ataupun fungsi wajib mendeklarasikan tipe data. Ketika suatu variabel telah memiliki tipe data maka ketika di assign dengan tipe data lain akan menimbulkan error.

#### Visibilitas
Seperti yang telah kita ketahui bersama penulisan visibilitas pada bahasa pemrograman PHP ditulis tepat sebelum penulisan _property_ atau _method_, dengan menggunakan kata kunci sesuai dengan tipe visibilitas yang ingin digunakan.

PHP mengenal 3 tipe visibilitas yaitu _public, private dan protected._ _Public_ artinya property atau method tersebut dapat diakses baik dari lingkup kelas maupun objek. _Private_ artinya property atau method yang nilainya hanya bisa diakses dari lingkup kelas dimana property atau method tersebut didefinisikan. _Protected_ artinya dapat di akases dari lingkup kelas dimana _property_ atau method tersebut di definisikan serta turunan dari kelas tersebut.

sedangkan **GO hanya memiliki 2 tipe visibilitas yaitu _public_ dan _private_**. _Public_ artinya dapat diakses dari mana saja, sedangkan _private_ hanya terbatas pada module yang bersangkutan. Untuk membedakan antara public dan private dalam penulisan huruf pertama menggunakan huruf Kapital.

#### Package & Namespace
Package dan namespace tidak jauh berbeda berbeda, keduanya bukanlah gambaran dari directory file tersimpan. Banyak manfaat dalam penggunaan package dan namespace diantaranya adalah untuk memudahkan dalam proses _export import_ fungsi, selain itu Keduanya memiliki fungsi yang sama yaitu untuk mengelompokkan kode (kelas, objek dan fungsi).

#### Dependency management
Dalam mengembangkan suatu aplikasi terkadang kita membutuhkan _package_ atau _library_ yang telah dibuat oleh pengembang lain. _package_ atau _library_ yang kita gunakan terkadang juga bergantung pada package lain, jika tanpa _dependency management_ kita akan dibuat sangat kerepotan dalam mengelola dependency aplikasi yang sedang kita kembangkan, maka dari itu terciptakan _dependency management_ yang dapat membantu dalam proses management dependency. PHP mempunyai **_composer_** sedangkan GO (v1.11) memiliki **_go-mod_**.

#### Function
GO dan PHP tidak bisa terlepas dari function, tidak banyak perbedaan antara function PHP dan Golang, yang menjadi perbedaan hanyalah GO dapat memberikan nilai kembalian lebih dari satu, berikut contohnya.

```GO
package main 
func myfunc(p, q int)(rectangle, square int ){ 
    rectangle = p*q 
    square = p*p 
    return  
}
```

#### Struct & Class
Secara garis besar antara Struct dan class memiliki suatu kesamaan yaitu sebagai _blueprint_ atau cetakan dari objek.

### Bonus
Untuk yang sedang memulai belajar bahasa GO berikut ini adalah beberapa _learning resource_ yang menjadi panduan saya dalam belajar GO sampai dengan sekarang. [Learning resource](https://dasarpemrogramangolang.novalagung.com/).
