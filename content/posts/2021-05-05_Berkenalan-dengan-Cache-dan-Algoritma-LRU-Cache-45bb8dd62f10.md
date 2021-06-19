---
title: "Berkenalan dengan Cache dan Algoritma LRU Cache"
tags:
  - LRU Cache
  - Cache 
categories: 
  - Algorithm
date: 2021-05-05T08:43:26+07:00
draft: false
description: API gateway merupakan perantara yang menghubungkan antara aplikasi client dengan tiap service yang tersedia.
---

Tingkatkan performance aplikasi menggunakan Algoritma LRU Cache

![](https://cdn-images-1.medium.com/max/800/1*molTyQ-WrpCj8lzlAph62g.jpeg)

Dalam pengembangan aplikasi modern, _cache_ merupakan suatu hal yang lumrah untuk diterapkan. _Cache_ berfungsi untuk meningkatkan _performance_ dari suatu aplikasi. Salah _software_ yang paling populer untuk mendukung penerapan _cache_ di aplikasi adalah Redis.

### Pengertian Cache

_Cache_ merupakan mekanisme penyimpanan data secara sementara dalam memori komputer, ketika ada permintaan data ke memori komputer maka data akan disediakan lebih cepat. Data yang disimpan merupakan data hasil proses komputasi yang dinilai memakan biaya tinggi dalam proses komputasinya (misal: koneksi ke basis data), atau bisa juga hasil data yang sering diakses dan jarang ada perubahan.

#### Kenapa harus menggunakan Cache?

1.  _Cache_ berguna untuk meningkatkan _performance_ aplikasi karena menyimpan data dalam memori komputer yang memiliki kecepatan tinggi.
2.  _Cache_ dapat meringankan kerja _processor_. Ketika ada 100 permintaan data yang identik di waktu yang bersamaan tanpa menerapkan _cache_, _processor_ harus memproses dan kalkulasi 100 permintaan data. Jika menggunakan _cache_, _processor_ hanya perlu memproses permintaan ke 1 lalu data hasil proses dan komputasi disimpan dalam _cache_ komputer, di permintaan selanjutnya _processor_ hanya perlu mengambil data yang telah disimpan dalam _cache_.

#### Studi Kasus penerapan Cache

Untuk mempermudah memahami _cache_, saya akan memberikan sebuah contoh studi kasus penerapan _cache_ pada suatu aplikasi.

Misal pada aplikasi _e-commerce_, ketika kita akan membeli suatu produk maka kita diarahkan untuk melakukan akses ke halaman detail produk yang akan kita beli. Misal URL-nya adalah.

`GET /sarangeofficial/sarange-phyto-cream`

Misal untuk mendapatkan semua data yang nantinya ditampilkan pada halaman detail produk terdapat banyak proses yang berat, selain itu sistem juga harus melakukan akses ke beberapa _service_, di antaranya:

1.  _Product service_
2.  _Customer review service_
3.  _Product recommendation service_

Setiap _service_ membutuhkan waktu 100ms untuk menyelesaikan tugasnya, jadi total yang waktu dibutuhkan 300ms/request untuk menampilkan semua data pada halaman detail produk.

![](https://cdn-images-1.medium.com/max/800/1*SHj1Bt50_xCnqUd6Zp9iIw.png)

Suatu aplikasi e-commerce tidak mungkin hanya diakses 1 user pada suatu waktu. Misal ada 100 user melakukan akses ke halaman detail produk yang sama, maka total waktu yang dibutuhkan komputer untuk melayani permintaan dari 100 user adalah 30000ms.

Tentu jika waktu yang dibutuhkan sebanyak itu maka user akan merasa bahwa aplikasi _e-commerce_ yang diakses sangat lamban. Pada saat ini penggunaan _cache_ akan sangat membantu dalam mempercepat proses.

![](https://cdn-images-1.medium.com/max/800/1*0xXSqzbRdpwW0mBTvfQa2w.png)

Misal untuk mengambil data dari _cache_ hanya dibutuhkan waktu 20ms, user pertama tetap membutuhkan waktu 300ms sampai _request_\-nya dipenuhi, namun _user_ setelahnya hanya membutuhkan waktu 20ms saja pada saat melakukan akses ke halaman detail produk sampai semua data ditampilkan.

Penggunaan _cache_ merupakan salah satu solusi untuk meningkatkan _performance_ aplikasi. Setiap solusi tentu ada _tradeoff_ yang harus dibayarkan, salah satunya adalah _cost_ dari memori itu sendiri. Selain itu data yang akan disimpan menjadi data _persistence_ dan memiliki keterbatasan kapasitas penyimpanan.

Maka dari itu untuk meningkatkan kinerja _cache_ dan menekan biaya penggunaan terdapat beberapa algoritma untuk melakukan _management cache_, salah satunya adalah _Least Recently Used._

#### LRU: Least Recently used

Merupakan suatu algoritma _page replacement_ yang sering digunakan dalam arsitektur komputer. Algoritma ini menerangkan bagaimana komputer melakukan manajemen memori dan alokasi memori sehingga proses di dalamnya menjadi lebih cepat.

> Jika diterjemahkan dalam bahasa Indonesia Lest recently used artinya “paling terakhir digunakan”

Sesuai namanya, cara kerja algoritma LRU adalah mengurutkan posisi _cache_ berdasarkan item yang paling baru digunakan dan menghapus _cache_ yang paling lama tidak dipakai jika telah melebihi kapasitas penyimpanan yang telah ditentukan.

Misal kita memiliki 5 kotak kosong dalam memori komputer, 5 kotak kosong ini akan digunakan sebagai tempat untuk menyimpan _cache_ dan menerapkan algoritma LRU untuk melakukan _management_ memori dan alokasi memori.

Ketika _insert_ data memiliki konsep yang mirip dengan Stack, setiap item baru akan berada pada urutan paling depan, dan akan menggeser +1 item yang sebelumnya menempati posisi depan jika ada.

![](https://cdn-images-1.medium.com/max/800/1*KIEqJ9WwQ3Dt1iNr0ZGxCA.png)

Lalu jika terjadi operasi _get_ atau mengambil data dari _cache_, data yang baru saja dibaca akan di**pindah ke urutan paling depan**, data lainnya akan digeser ke belakang dengan index+1. Perhatikan gambar berikut ini untuk mempermudah memahami konsep ketika operasi _get_ data.

![](https://cdn-images-1.medium.com/max/800/1*ESw5voAZag7muraCsdAZ0w.png)

Konsep terakhir dari algoritma LRU adalah jika terjadi penambahan data tetapi kapasitas data yang dapat disimpan telah sesuai dengan kapasitas maksimal, maka data yang akan dihapus adalah data yang paling lama tidak digunakan, atau untuk memudahkan adalah data yang posisinya berada paling belakang.

![](https://cdn-images-1.medium.com/max/800/1*c1GQT96GTOIbub-DUv4cBg.png)

Di luar sana banyak aplikasi yang memanfaatkan Algoritma LRU, salah satunya adalah Redis yang merupakan aplikasi _Cache_ paling populer saat ini. Untuk mengetahui bagaimana Redis menerapkan LRU dapat mengikuti artikel [berikut](https://redis.io/topics/lru-cache).

#### Kesimpulan

*   _Cache_ merupakan salah satu solusi untuk meningkatkan performa aplikasi.
*   _Cache_ memanfaatkan memori sebagai media penyimpanan data.
*   Terdapat banyak algoritma untuk _management_ data pada _cache_, salah satunya Algoritma _Least Recently used_.

Original post By [Asdita Prasetya](https://medium.com/@hellodit) on [Medium](https://medium.com/@hellodit/berkenalan-dengan-cache-dan-algoritma-lru-cache-45bb8dd62f10).
