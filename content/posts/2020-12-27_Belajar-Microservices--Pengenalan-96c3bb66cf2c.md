---
title: "Belajar Microservices: Pengenalan"
tags:
  - Software Engineering
categories: 
  - Software Architecture
  - Microservices
date: 2020-09-24T08:43:26+07:00
draft: false
description: Microservices merupakan metodologi dalam pengembangan perangkat lunak dengan memisahkan suatu aplikasi yang besar menjadi beberapa aplikasi yang lebih sederhana.
---


Bagian pertama dari seri belajar microservice

![](https://cdn-images-1.medium.com/max/800/0*E8EpaH8BzdlA2EqV)

Dalam pembuatan aplikasi banyak aspek yang perlu diperhatikan, salah satunya adalah arsitektur aplikasi, belakangan ini arsitektur _microservice_ banyak di perbincangkan, arsitektur ini telah terbukti memecah kerumitan dalam pengembangan aplikasi, terutama aplikasi _web services,_ telah banyak perusahaan yang sukses dengan implementasi _microservice_ contohnya adalah [Netflix](https://www.nginx.com/blog/microservices-at-netflix-architectural-best-practices/), Amazon dan [eBay](https://dzone.com/articles/microservices-at-ebay-part-2-sharing-modules-acros).

Selain arsitektur _microservice_ ada juga arsitektur monolitik. arsitektur monolitik dan microservice memiliki kelebihan dan kekurangan masing — masing, penerapan-nya pun di sesuaikan dengan kebutuhan bisnis dari aplikasi.

### Arsitektur Monolitik

Jika yang dibahas mengenai arsitektur aplikasi, maka kita mengesampingkan bahasa yang digunakan dalam membangun aplikasi.

Kita asumsi-kan akan **membuat suatu web service untuk aplikasi penyewaan sepeda yang akan di beri nama “Onthel”**, setelah melalui banyak rapat dengan tim menentukan fitur apa saja yang harus ada dan melakukan riset pasar maka jadilah arsitektur aplikasi yang akan dibuat seperti dibawah ini.

![](https://cdn-images-1.medium.com/max/800/1*5myyqLpI3JQJ3_XN0RQtIw.png)

Dalam satu codebase aplikasi Onthel terdapat kode untuk menangani _user interface, business logic_ dan _data access layer._ Selain itu memiliki satu database yang akan menyimpan data pengguna, order, sepeda dan riwayat perjalanan.

Aplikasi dengan arsitektur monolitik sangatlah umum, membangun aplikasi dengan **arsitektur monolitik memiliki banyak keuntungan**, diantaranya adalah:

1.  Aplikasi lebih mudah dalam proses pengembangan, hal ini karena kebanyakan code editor atau IDE yang kita gunakan lebih banyak yang fokus dalam mendukung proses pengembangan aplikasi dengan arsitektur monolitik
2.  Lebih mudah dan cepat dalam proses pengujian, semudah menjalankan aplikasi lalu melakukan pengujian manual maupun dengan bantuan perangkat lunak lain seperti Selenium
3.  Aplikasi lebih mudah dalam proses _deploy,_ cara paling sederhana dengan menyalin kode ke server melalui Git atau dengan bantuan FTP client. Ketika proses telah selesai maka aplikasi yang kita buat sudah siap untuk dijalankan.
4.  Mudah dalam proses _scaling_, misalnya menjalankan beberapa salinan dari aplikasi dengan menggunakan bantuan _load balancer._

Pada awal rilis dengan arsitektur monolitik semua berjalan dengan lancar, semua fitur berjalan, performa aplikasi juga sangat baik. Hari berganti hari, tahun pun berganti Onthel menjadi aplikasi yang sangat populer dan memiliki banyak pengguna, bahkan pengguna aplikasi Onthel hampir sama dengan pengguna aplikasi Gojek.

Dengan suksesnya aplikasi Onthel maka tim developer berniat untuk menambahkan berbagai fitur baru, aplikasi yang awalnya sederhana kini menjadi aplikasi yang besar, dari 1000 baris kode kini bertambah 10x baris kode, belum lagi ditambah dengan _dependecy_ semakin besar di aplikasi Onthel.

Aplikasi Onthel kini menjadi aplikasi monolith yang besar dan memiliki banyak fitur di dalamnya, penerapan arsitektur monolith menjadi tidak cocok lagi karena:

1.  Semakin besar aplikasi maka waktu untuk _start-up_ menjadi semakin lama.
2.  Akan terjadi kendala ketika menerapkan _continuous deployment._
3.  Aplikasi tidak dapat dikembangkan dengan bebas karena adanya kendala dalam menerapkan suatu bahasa dan adanya kendala dalam penentuan spesifikasi hardware yang cocok.
4.  Jika suatu fitur mengalami gangguan maka fitur lain bisa saja terpengaruh, lebih parahnya aplikasi bisa _crash_ sehingga mengganggu proses bisnis yang berjalan.

Aplikasi yang besar dan memiliki banyak fitur akan sangat susah dikembangkan jika menggunakan arsitektur Monolithic maka dari itu solusinya adalah dengan menggunakan **arsitektur microservice.**

### Arsitektur _Microservice_

Pemisahan suatu aplikasi yang besar menjadi beberapa aplikasi yang lebih sederhana, beberapa aplikasi yang di pisah akan saling berkomunikasi untuk melayani pengguna. Aplikasi yang lebih kecil dan sederhana dalam bahasan _microservice akan disebut sebagai service._

Dalam implementasi _microservice_ tiap _service_ memiliki fungsi yang spesifik. Misalnya hanya memiliki fungsi untuk melayani pembayaran. Gambar dibawah ini menunjukan secara sederhana arsitektur microservice:

![](https://cdn-images-1.medium.com/max/800/1*ZtS-hq4jort2XQr3fcALIw.png)

Dalam implementasi-nya tiap service dapat memiliki basis data berbeda dengan service lain, tiap service akan saling berkomunikasi dengan service lain melalui API Gateway. Dengan menggunakan arsitektur _microservice_ aplikasi akan menjadi:

1.  Waktu _start-up_ service menjadi lebih cepat.
2.  Aplikasi yang semula rumit menjadi lebih sederhana dan mudah untuk dikembangkan.
3.  Setiap _service_ berjalan dengan _independent_ tidak tergantung dengan _service_ lain, jika ada satu _service_ mengalami gangguan maka kecil kemungkinan aplikasi akan mengalami _crash_.
4.  Performa _service_ lebih handal karena setiap service dapat di install di hardware yang sesuai.
5.  Aplikasi dapat dibuat dengan berbagai macam bahasa dan framework sesuai dengan kebutuhan service.
6.  Dapat menggunakan berbagai jenis basis data penyimpanan.

#### Kesimpulan

Pemilihan penggunaan arsitektur sangatlah penting dalam pembuatan web service, baik monolitik maupun _mikroservice_ memiliki kekurangan dan kelebihan masing — masing, aplikasi yang sederhana lebih cocok untuk menggunakan arsitektur monolitik, sedangkan aplikasi yang sekalanya besar sangat disarankan untuk menggunakan arsitektur _microservice._

Posted on medium by [Asdita Prasetya](https://medium.com/@hellodit) on [December 27, 2020](https://medium.com/p/96c3bb66cf2c).

