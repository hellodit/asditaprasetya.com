---
title: "API Gateway untuk Pengembangan Microservice"
tags:
  - Software Engineering
  - API Gateway
categories: 
  - Software Architecture
  - Microservices
date: 2021-02-28T08:43:26+07:00
draft: false
description: API gateway merupakan perantara yang menghubungkan antara aplikasi client dengan tiap service yang tersedia.
---

![](https://cdn-images-1.medium.com/max/800/0*aoZyC0Z8qPFKFBeS)

Seperti yang sudah saya tuliskan [sebelumnya](https://hellodit.medium.com/belajar-microservices-pengenalan-96c3bb66cf2c) bahwa aplikasi yang menggunakan arsitektur _microservice_ terdiri dari banyak aplikasi yang berdiri sendiri sesuai dengan tugasnya. Ketika membangun suatu aplikasi _microservice_ perlu dipikirkan dengan matang bagaimana aplikasi _client_ berinteraksi dengan aplikasi _server_.

Pada aplikasi monolitik aplikasi _client_ hanya perlu untuk berkomunikasi dengan satu set _endpoint_ pada semua bisnis proses yang dapat dilakukan oleh aplikasi, selanjutnya dapat di replikasi oleh load balancer untuk mendistribusikan lalulintas di antara mereka, namun hal ini tidak berlaku pada aplikasi yang menerapkan arsitektur microservice.

Untuk lebih mudah memahami bagaimana aplikasi _client_ dan aplikasi _server_ saling berkomunikasi maka kita buat studi kasus.

Suatu saat saya ingin membeli _powerbank_ di suatu ecommerce, saya membuka _web browser_ kemudian masuk ke halaman detail produk _powerbank_ yang ingin saya beli, anggap saja halaman yang saya buka adalah `http://tukupedia.com/powerbank/powerbank-murah-meria` nah di halaman detail produk yang akan saya beli akan menampikan informasi berupa:

1.  Detail produk
2.  Rewiew produk
3.  Rekomendasi produk sejenis
4.  Riwayat pencarian produk
5.  dan yang lainnya

Kita asumsikan tukupedia menggunakan arsitektur monolitik, maka ketika saya membuka halaman detail produk, aplikasi client akan melakukan permintaan data melalui API detail produk untuk mendapatkan semua informasi.

Misal meminta data melalui API dengan melakukan akses ke`GET [api.company.com/products/id]` lalu _service backend_ malukan query ke basis data dan mengembalikan hasil data untuk ditampilkan melalui aplikasi aplikasi client, sangat sederhana dan mudah.

Dengan menggunakan arsitektur microservice data yang ingin ditampilkan pada aplikasi client dimiliki oleh berbagai service yang berbeda diantaranya:

1.  _Product service_
2.  _Customer review service_
3.  _Product recommendation service_
4.  _Search history service_

Lalu bagaimana cara aplikasi _client_ untuk mendapatkan data yang dimiliki oleh berbagai service yang berbeda?

### Aplikasi client melakukan akses langsung ke tiap service

Aplikasi _client_ melakukan permintaan data ke tiap _service_ secara langsung dengan akses ke tiap _endpoint_ yang tersedia, dengan cara ini aplikasi _client_ harus bisa menangani setiap permintaan yang dibuatnya, pada studi kasus kita _client_ harus melakukan permintaan ke 4 service yang berbeda, hal ini membuat aplikasi client yang dibuat akan lebih kompleks dan besar.

Lalu bagaimana jika makin banyak service yang di akses secara langsung? semakin kompleks juga aplikasi client yang dibuat dan mempersulit pengembangan aplikasi client. Gambar dibawah ini merupakan ilustrasi komunikasi langsung antara aplikasi client dan aplikasi server

![](https://cdn-images-1.medium.com/max/800/1*sSgmsElRFZ1Nv6FIEKomvw.png)

Permasalahan lainnya adalah tidak semua service menggunakan protocol yang _web friendly,_ misalkan ada service yang menggunakan GRPC atau mungkin ada yang menggunakan AMQP sebagai _messaging protocol_.

Melakukan akses langsung ke tiap service mengakibatkan service menjadi lebih rumit untuk dikembangkan. Misalnya suatu saat diperlukan pengembangan _customer review service_, untuk meningkatkan performance dan ketersediaan, customer review service_ akan dipecah menjadi service yang lebih kecil lagi, maka selain melakukan refactor _Customer review service_ developer juga harus melakukan refactoring pada aplikasi client, hal ini akan memperlambat proses pengembangan suatu produk.

Dalam dunia microservice akses langsung ke tiap service sangat tidak direkomendasikan, maka dari itu diperkenalkan konsep API Gateway.

### Menggunakan API gateway

API gateway merupakan perantara yang menghubungkan antara aplikasi client dengan tiap service yang tersedia, konsep API gateway mirip dengan FACADE pattern pada konsep pemrograman berbasis objek.

> The API Gateway is responsible for request routing, composition, and protocol translation. All requests from clients first go through the API Gateway. It then routes requests to the appropriate microservice. The API Gateway will often handle a request by invoking multiple microservices and aggregating the results It can translate between web protocols such as HTTP and WebSocket and web-unfriendly protocols that are used internally — Nginx

Pada studi kasus kita client hanya perlu melakukan akses ke satu endpoint untuk mendapatkan semua data yang akan ditampilkan pada halaman produk, API gateway bertugas untuk menangani request dan meneruskan request ke service yang bersangkutan, lalu melakukan agregasi respond dari tiap service kemudian dikembalikan ke client, untuk kemudian ditampilkan ke user.

Dengan menggunakan API gateway akan memudahkan developer aplikasi client dan aplikasi server, client tidak perlu menangani banyak request dan aplikasi server pun akan lebih mudah dan fleksibel dalam proses pengembangan.

![](https://cdn-images-1.medium.com/max/800/1*pVlF16KV_Z7tfFpAxTWFtQ.png)

### Syarat utama yang harus dimiliki API gateway:

#### Performance and Scalability

Performa dan skalabilitas menjadi poin utama yang menjadi perhatian dalam pembuatan API gateway, untuk itu maka dalam pengembangannya diwajibkan untuk mendukung proses asynchronous, non blocking I/O.

#### Service Invocation

Untuk berkomunikasi dengan service lain API gateway harus menerapkan _inter-process communication mechanism._ Komunikasi antar service dalam diraih dengan cara asynchronous maupun dengan komunikasi langsung

#### Service Discovery

API Gateway harus bisa mengetahui alamat dari suatu _service_ baik IP dan port, hal ini harus dilakukan secara dinamis dan otomatis, karena dalam implementasinya jika di lakukan _scaling_ maupun upgrade alamat IP dan port akan berubah.

#### Handling Partial Failures

Ketika salah ada service yang terhubung ke API gateway mengalami error atau tidak bisa diakses, maka API gateway di wajibkan untuk memiliki kemampuan untuk menanganinya, misalnya ketiak suatu service rekomendasi produk mengalami kegagalan API gateway di wajibkan untuk tidak melalukan blocking pada service yang bergantung service rekomendasi produk. kasus lain jika suatu service sedang tidak tersedia API gateway bisa saja memberikan cache data jika tersedia.

Perlu menjadi catatan dalam penggunaan API gateway adalah mengenai ketersediaan dan keamanan, API gateway harus menjadi anak emas dalam proses pengembangan karena memiliki tugas yang sangat penting.

### Kesimpulan

API gateway digunakan untuk mempermudah komunikasi antara aplikasi client dan aplikasi server, dengan menggunakan API gateway client akan terhindar dari kerumitan dengan berkomunikasi langsung ke setiap service yang berbeda. Selain itu aplikasi server juga akan lebih mudah untuk dikembangkan karena tidak terikat dengan aplikasi client secara langsung.

Original post By [Asdita Prasetya](https://medium.com/@hellodit) on [Medium](https://medium.com/@hellodit/api-gateway-untuk-pengembangan-microservice-d4cefd4607a6)
