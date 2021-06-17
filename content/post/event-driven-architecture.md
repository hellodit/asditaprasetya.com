---
title: Event-Driven Architecture
slug: update-slug
tags:
  - foo
  - bar
date: 2021-06-11T08:43:26+07:00
draft: false
description: Event-Driven Architecture description
---

![](https://cdn-images-1.medium.com/max/800/0*fQIB3IIPjJocglPW)

Dalam membangun suatu sistem dengan arsitektur _microservice_ kita perlu menentukan metode yang tepat untuk menjembatani komunikasi antar _service_ yang saling terpisah dan berdiri sendiri, terkadang ada service yang perlu terhubung ke service lain untuk menyelesaikan suatu proses bisnis.

Anggap saja, kita memiliki aplikasi eCommerce dengan menggunakan arsitektur _microservice_ yang didalamnya terdapat aplikasi pemesanan, pembayaran, pemberitahuan, whist list dan review.

Pada proses pemesanan tiap _service_ yang terkait akan saling berkomunikasi untuk menyelesaikan proses pemesanan yang dilakukan oleh pelanggan. Aplikasi pemesanan akan berkomunikasi dengan aplikasi pembayaran untuk membuatkan _invoice_ lalu berkomunikasi lagi dengan aplikasi pemberitahuan yang akan mengirim email ke pelanggan.

Secara umum ada dua jenis cara integrasi di _microservice_, yaitu :

*   _API-Driven Architecture_
*   _Event-Driven Architecture_

Kali ini saya akan membahas secara singkat mengenai _Event-Driven Architecture_

### Arsitektur Event-Driven

Sebelum melangkah lebih jauh kita harus mengetahui apa yang di maksud dengan _Event_, karena menggunakan bahasa inggris maka saya mengambil pengertian _Event_ dari Oxford dictionary.

> _Event is A thing that happens, especially something important_

Jika di artikan dalam bahasa Indonesia dan di sesuaikan dengan pembahasan arsitektur _microservice_ maka event adalah suatu kejadian yang terjadi terutama suatu yang bersifat penting, misal perubahan dari suatu kondisi yang dapat dikenali. Contohnya data sensor, log, transaksi, atau event klik website.

#### **Apa yang dimaksud dengan arsitektur event-driven?**

Suatu arsitektur perangkat lunak dan model design aplikasi yang menangkap _event_ yang terjadi pada suatu aplikasi, nantinya _event_ yang ter-_capture_ akan digunakan sebagai mekanisme integrasi antar aplikasi.

#### **Bagaimana arsitektur event-driven bekerja?**

Dalam event-driven architecture terdapat 3 komponen utama yang saling terhubung satu sama lain, ketiga komponen yang dimaksud yaitu:

1.  _Event producer,_ mendeteksi dan memproduksi event yang berlangsung pada suatu aplikasi lalu merepresentasi-kan sebagai pesan yang akan dikirim ke _platform processes_ atau _message broker, p_roses pengiriman _event_ biasanya berlangsung secara _asynchronously_,
2.  _Message broker,_ merupakan komponen pada arsitektur _event-driven_ yang bertugas sebagai _middleware_ antara _event producer_ dan _event consumer,_ tugas utamanya adalah untuk mengirim message yang dibuat oleh _event producer_ ke _event consumer._
3.  _Event consumer,_ komponen yang menerima _message_ yang dikirim oleh _message broker_ kemudian melakukan proses sesuai dengan perintah yang ada dalam pesan yang diterima.

![](https://cdn-images-1.medium.com/max/800/1*cN8MsEVTSDpeWlLfTZveGg.png)

#### **Choreography Pattern**

Arsitektur _Event-Driven_ berkaitan erat dengan _choreography pattern_, tiap service atau aplikasi harus tahu apa yang akan dilakukan ketika ada suatu yang terjadi. Setiap action yang dilakukan oleh service harus sesuai dengan domain-nya, service akan berjalan secara mandiri untuk menyelesaikan tugas yang di delegasi-kan oleh service lain. Gambar dibawah ini menunjukan proses chcoreography yang terjadi ketika order di buat pada suatu sistem eCommerce.

![](https://cdn-images-1.medium.com/max/800/1*RU-txT1PUN-gn7FRAzO-gg.png)

Untuk memudahkan pemahaman kita ambil studi kasus penari, sebagai seorang penari dalam keseharian di tuntut untuk tahu gerakan yang harus dilakukan sesuai dengan kejadian yang sedang berlangsung, salah satunya berdasarkan musik yang sedang diputar.

Choreography pattern akan mempermudah dalam pengembangan suatu sistem, ketika ada service baru yang perlu di terapkan dalam sistem sercive dapat memperoleh data dari service yang sudah ada hanya dengan terhubung dengan message broker, tanpa harus mengubah semua kode pada service yang sudah tersedia.

#### Keuntungan menggunakan arsitektur event-driven

1.  Tidak ada ketergantungan, tiap service tidak saling bergantung dengan service lain. Sehingga dalam proses pengembangan service dapat menghindari _bottleneck_ antar team development, selain itu dapat menghindari terjadinya masalah pada _service_ yang disebabkan oleh _service_ lain.
2.  Menurunkan waktu response, jika di bandingan dengan _API-Driven Architecture_ dengan menggunakan Resfull API sebagai media komunikasi, Event-Driven Architecture dapat memberikan waktu response yang lebih cepat, hal ini terjadi salah satunya karena komunikasi antar service yang bersifat [**asynchronous**](https://medium.com/catatan-javascript/memahami-synchronous-dan-asynchronous-457fdd4c35d)**.**
3.  High Availability, karena tiap service berdiri sendiri, jika ada service yang mengalami masalah maka service lain tidak akan terpengaruh. Selain itu akan ada mekanisme **_recovery service_** _jika terdapat service yang terkena masalah,_ topik ini akan di bahas selanjutnya.

### Kesimpulan

1.  _API-Driven Architecture_ dan _Event-Driven Architecture_ merupakan metode untuk melakukan integrasi antar service dalam arsitektur _microservice_
2.  Arsitektur Event-Driven merupakan arsitektur yang bekerja berdasarkan event yang di deteksi oleh _event producer_
3.  Terdapat 3 komponen utama dalam arsitektur Event-Driven yaitu producer, broker dan consumer
4.  Event-Driven Architecture menggunakan metode asynchronous untuk melakukan komunikasi antar service

#### Bonus

Jika ingin mengetahui lengkap mengenai Event-Driven dapat membuka tautan berikut ini:

1.  [Micoservice.io](https://microservices.io/patterns/data/event-driven-architecture.html)
2.  [gist.github.com](https://gist.github.com/giampaolotrapasso/71221f378770e21e6270ffed76b181d7)
3.  [tibco.com](https://www.tibco.com/reference-center/what-is-event-driven-architecture)
