---
title: My Commit Message History
tags:
  - Software Engineering
categories: 
  - Self Documentation
date: 2020-10-25T08:43:26+07:00
draft: false
description: Perjalanan penulisan commit message dari pertama sampai saat ini

---

![](https://cdn-images-1.medium.com/max/800/0*LO6fsVwIYdtH_Vr9)

Sebagai developer saya rasa istilah Git sudah tidak asing lagi, Git merupakan _distributed version control system_ artinya _version control_ yang media penyimpanan tidak hanya pada satu komputer saja. Dengan menggunakan Git akan memudahkan developer untuk bekerja dengan developer lainnya dalam suatu tim selain itu penggunaan Git akan membuat aplikasi lebih mudah untuk di Deploy, untuk mengetahui apa saja kegunaan Git dalam proses pengembangan perangkat lunak silahkan mengikuti tautan yang saya sertakan di akhir artikel.

#### Git _commit message_

Salah satu hal yang paling penting dalam penggunaan Git adalah _commit message_. _Commit message_ digunakan untuk menandai suatu perubahan yang dilakukan pada baris kode tertentu, _commit message_ juga digunakan untuk melihat riwayat dari suatu suatu baris kode atau secara keseluruhan.

Maka dari itu penulisan _commit message_ diharuskan dapat menjelaskan mengenai perubahan apa yang dilakukan, hal ini akan memudahkan kerja team karena setiap anggota menjadi mengerti kenapa terjadi perubahan pada kode. Namun menentukan _commit message_ tidaklah mudah karena setiap orang dalam satu team memiliki gaya sendiri dalam penulisan.

### Pertama kali belajar Git

Tahun 2018 merupakan awal saya belajar menggunakan Git, pada saat itu tidak terpikir menganai bagaimana menuliskan commit message yang dapat dengan mudah dimengerti orang lain, pokoknya asalkan menurut saya sudah mendeskripsikan perubahan yang saya lakukan maka itu sudah benar.

Misal saya merubah kode untuk melakukan _bug fixing_ maka yang saya tulis adalah “_Bug fix_” namun ini tidak baik karena tidak secara jelas mendeskripsikan apa yang telah saya lakukan.

![](https://cdn-images-1.medium.com/max/800/1*1BFL-huYuqqJBJzFMQ2TYQ.png)

### Commit message versi 2

Di akhir tahun 2018 saya mendapatkan kesempatan untuk mengikuti _bootcamp_ **_Binar Academy_**, saya termasuk siswa di _Batch 8_ dari Yogyakarta. Pada waktu itu ada 1 pertemuan di khususkan untuk membahas Git, salah satunya topik yang dibahas adalah bagaimana menuliskan _commit message_, disana saya dikenakan dengan _commit conversion._

_Commit conversion_ merupakan suatu ketetapan dalam menulis _commit message_ yang di sepakati, di ketahui dan di terapkan oleh seluruh anggota tim, dengan adanya ketetapan bersama, seluruh anggota tim diharapkan akan membentuk suatu standarisasi yang nantinya akan memudahkan tim dalam bekerja, Berikut ini adalah penulisan commit message yang saya lakukan.

![](https://cdn-images-1.medium.com/max/800/1*JN07LnYY-EWIWJ6qCIB9XQ.png)

### Commit message versi 3

Beberapa bulan yang lalu tepatnya di bulan Oktober 2020 saya mencoba untuk menerapkan _commit convention_ yang baru saya pelajari dari [**conventionalcommits.org**](http://conventionalcommits.org/) disana dijelaskan mengenai bagaimana cara penulisan yang sesuai dan kenapa harus di tulis seperti itu, selain itu ada beberapa _tools_ pendukung yang mana memanfaatkan _commit convention_ yang telah ditulis, misalnya membuat _changelog_ secara otomatis.

Menurut saya ini adalah format yang paling sesuai sampai saat ini untuk diterapkan dalam proses pengembangan perangkat lunak. Contoh dari aturan penulisannya adalah sebagai berikut.

```
<type>[optional scope]: <description>[optional body][optional footer(s)]
```

Benar, setelah saya terapkan saya menjadi lebih mudah mengerti tentang apa saja riwayat perubahan dari kode yang saya tuliskan.

![](https://cdn-images-1.medium.com/max/800/1*-PN1GIDAVVG4i3weNYHj0A.png)

Jika tertarik untuk belajar lebih lanjut silahkan kunjungi tautan yang saya sertakan di paling bawah.

### Bagaimana seharusnya menuliskan commit message?

Sebagai rangkuman dari artikel singkat yang saya tulis kali ini, kunci dari penulisan _commit message_ adalah **penulisan secara deskriptif dan singkat sehingga mudah dipahami oleh diri dan orang lain sendiri di masa depan.**

### Resources 
- [Git Documentation](https://git-scm.com/doc)
- [Commit conventional](https://www.conventionalcommits.org/en/v1.0.0/)


Original post from [Medium](https://medium.com/@hellodit/my-commit-message-history-3f7cd528f389) on December 12, 2020