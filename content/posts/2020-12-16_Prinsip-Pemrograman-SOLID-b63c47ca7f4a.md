---
title: Prinsip Pemrograman SOLID
tags:
  - Design Pattern
  - Software Engineering
categories: 
  - Software Architecture
date: 2020-12-16T08:43:26+07:00
draft: false
description: SOLID The First 5 Principles of Object-Oriented Design.
---




![](https://cdn-images-1.medium.com/max/800/1*tCjzLJkEb6UqpNYi0HNktQ.jpeg)

Pengembangan perangkat lunak merupakan suatu proses yang dilakukan secara tim, sangat jarang perangkat lunak yang kompleks hanya dikerjakan oleh satu orang. Bekerja dalam tim tidaklah semudah bekerja sendiri.

Maka untuk memudahkan pekerjaan tim, setiap anggota harus memiliki pengetahuan tentang cara menulis kode dengan baik dan benar sehingga kode yang ditulisnya dapat dimengerti oleh anggota tim lain dan mudah untuk dikembangkan suatu saat nanti.

Pada tahun 2000-an Robert C Martin melalui publikasinya yang berjudul “_Design Principle and Design Pattern_” memperkenalkan konsep SOLID. Konsep ini bertujuan untuk menghasilkan kode yang _reusebale, maintainable, scalable,_ dan _testable,_ selain itu menerapkan konsep SOLID juga akan mempermudah _software engineer_ bekerja dalam tim.

> **Peringatan!!** Berhenti di sini jika Anda belum mengerti _Object Oriented Programming_ (OOP).

### What is SOLID?

SOLID merupakan singkatan dari _Single-responsibility principle, Open-closed principle, Liskov substitution principle, Interface segregation principle_ dan _Dependency Inversion Principle._ Mari kita bahas satu persatu tentang konsep SOLID.

#### Single responsibility principle

_“A Class should be responsible for a single task or a class must have a specific purpose.”_

Suatu _class_ **tidak diperbolehkan** untuk mengerjakan banyak hal. Misalnya di dalam _class_ _invoice_ terdapat fungsi untuk mencetak _invoice_, akses basis data, dan melakukan perhitungan _order_. Hal ini sangat bertentangan dengan _Single responsibility principle._

_Single responsibility principle_ artinya _s_etiap _class_ **wajib** **hanya** memiliki satu tanggung jawab, dan hanya memiliki satu alasan untuk diubah. Contoh _class_ untuk mendefinisikan struktur data hanya akan diubah jika terdapat perubahan pada struktur data, atau _class_ yang mendefinisikan _business logic_ hanya akan diubah jika terjadi perubahan _business logic._

Salah satu implementasi dari _Single responsibility principle_ adalah _Repository Pattern._ Penjelasan singkat dan implementasi _Repository pattern_ pernah saya bahas di artikel sebelumnya (bisa dibaca di link bawah).

[Secara singkatnya Repository Pattern ...](https://medium.com/tlabcircle/implementasi-repository-pattern-dengan-laravel-8-be32eaacbe2d)

#### Open-closed principle
_“Software_ _entities should be open for extension but closed for modification or the short_”

Dengan menerapkan _Open-close principle_ kita harusnya bisa menambahkan fitur baru tanpa harus mengubah kode lama yang sudah ditulis sebelumnya. Hal ini dapat dilakukan dengan melakukan abstraksi yang tepat pada saat perancangan penulisan kode. Gunakan _interface_ dan atau _abstract classes. Open-closed Principle_ memaksa kita untuk menulis kode yang modular.

Mengubah kode yang telah ditulis sebelumnya dikhawatirkan akan menimbulkan _bug_ di _production._ Selain itu, perlu dilakukan pengulangan _testing_ pada kode lama yang seharusnya bisa dihindari jika menerapkan _Open-closed Principle._

#### Liskov substitution principle

_“Objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program.”_

Konsep ini terkait dengan proses _inheritance_ suatu fungsi atau objek. Dalam _Liskov substitution principle, super class_ harus dapat digantikan dengan objek dari _subclass_\-nya tanpa berefek pada suatu aplikasi. Hal ini dapat dilakukan dengan membuat objek dari _subclass_ memiliki perilaku sama dengan _superclass_, misalnya parameter dan _return value_ yang sama dengan _superclass_.

#### Interface segregation principle

_“A client should not be forced to use an interface if it doesn’t need it._”

Dalam bahasa Inggris _segregation_ memiliki arti _keeping things separated._ jika dikaitkan dengan _Interface segregation principle,_ maka artinya pemisahan _interface_.

Dalam pembuatan _interface,_ lebih baik membuat banyak _interface_ dengan fungsi yang spesifik. Hal ini lebih baik daripada membuat satu _interface_ dengan fungsi yang tidak spesifik. Tujuan dari pemisahan _interface_ adalah agar tidak memaksa _client_ menggunakan kode yang tidak diperlukan.

Jika sudah ada _interface_ yang tersedia, jangan menambahkan kode baru di _interface._ Lebih baik menambah _interface_ baru yang masih berhubungan dengan _interface_ lama, kemudian melakukan _implement._ Lagi pula satu _class_ dapat melakukan implementasi lebih dari satu _interface_, jadi manfaatkan itu.

#### Dependency inversion principle

Dalam _principle_ ini terdapat 2 aturan, yaitu:

1.  _High-level modules should not depend on low-level modules, both should depend on abstraction._
2.  _Abstractions should not depend on details. Details should depend on abstractions_

Setiap _class_ yang memiliki kompleksitas tinggi tidak boleh bergantung pada _class_ yang memiliki kompleksitas rendah, dan untuk melakukan komunikasi setiap kelas harus melalui abstraksinya (_interface_).

#### Penutup

Konsep SOLID wajib dipahami oleh setiap _software engineer_ setelah mempelajari _Object Oriented Programming_ (OOP). Dengan implementasi konsep SOLID ini, maka kode yang ditulis akan lebih _reusebale, maintainable, scalable,_ dan _testable._

#### Reference

[**S.O.L.I.D: The First 5 Principles of Object Oriented Design | DigitalOcean** ](https://www.digitalocean.com/community/conceptual_articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design)

[**SOLID Principles: Explanation and examples**](https://itnext.io/solid-principles-explanation-and-examples-715b975dcad4)

Original post from [Medium](https://medium.com/@hellodit/prinsip-pemrograman-solid-b63c47ca7f4a) on December 12, 2020
