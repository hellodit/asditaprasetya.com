---
title: "Membuat Aplikasi Cuaca dengan Speech Recognition"
tags:
  - Tutorial
  - Python
categories: 
  - Artificial Intelligence
date: 2021-02-03T08:43:26+07:00
draft: false
description: Speech recognition atau pengenalan suara bisa digunakan untuk melakukan pendeteksian cuaca di suatu daerah.
---

Speech recognition atau pengenalan suara bisa digunakan untuk melakukan pendeteksian cuaca di suatu daerah.

![](https://cdn-images-1.medium.com/max/800/1*YjuBZlFPBWC9A1gR6O2CXA.jpeg)

_Speech recognition_ atau pengenalan suara merupakan salah satu dari implementasi kecerdasan buatan (AI). Teknologi _speech recognition_ memungkinkan sistem komputer untuk memahami dan mengenali kata — kata yang diucapkan oleh manusia. _Speech recognition_ digunakan sebagai inti dari aplikasi asisten pribadi yang saat ini ada di ponsel pintar maupun di komputer, misal Siri, Google Assistant dan Amazon Alexa.

Komponen utama dari _Speech recognition_ adalah suara itu sendiri. Suara yang dicapkan oleh manusia dikenal sebagai gelombang analog. Dari gelombang analog yang diterima _microphone_ yang tersambung dengan komputer itulah untuk kemudian diubah menjadi gelombang elektrik melalui proses digitalisasi. Selanjutnya, hasil dari proses tersebut diekstrak datanya untuk dibandingkan nilainya dengan data model yang telah tersedia, sehingga sinyal digital dapat diterjemahkan menjadi teks.

Pada umumnya proses pengenalan suara melalui 3 tahapan, di antaranya:

#### Analisis Feature

Dalam proses Analisis _Feature, signal_ suara yang telah melalui proses digitalisasi dipotong per 10 milidetik untuk diambil nilai vektor yang mewakili.

#### _Unit Matching System_

Proses ini menggunakan pendekatan **Hidden Markov Model (HMM)**. Pendekatan ini mengasumsikan bahwa _signal_ ucapan yang telah didigitalisasi jika dilihat dalam waktu yang lumayan pendek dapat dikatakan sebagai proses _stationary —_ yaitu, proses yang mana properti statistik tidak berubah seiring waktu

_Unit matching system_ bertugas untuk mengenali dan mengamati _feature_ dari sinyal digital suara dengan menggabungkan informasi dari model akustik, model bahasa dan _Lexicon_.

*   Model akustik merupakan kumpulan file yang mendeskripsikan _variability_ vektor fitur.
*   Model bahasa merupakan sekumpulan data _probabilistic_ yang ditetapkan untuk mewakili suatu urutan kata.
*   _Lexicon_ adalah kosakata bahasa yang terdiri dari kata dan ungkapan. Leksikon juga bisa disebut kamus bahasa.

#### _Post Processor_

Pada proses ini _signal_ suara yang telah berhasil diterjemahkan kemudian diproses kembali menjadi aplikasi yang diinginkan, misalnya jika digabungkan dengan perangkat IOT maka kita dapat mematikan atau menghidupkan listrik rumah menggunakan perintah suara.

Jika ingin membaca lebih lanjut mengenai _Speech recognition,_ dapat membaca [Deep Learning for NLP and Speech recognition](https://link.springer.com/book/10.1007/978-3-030-14596-5) dan [CMUSphinx Tutorial](https://cmusphinx.github.io/wiki/tutorial/).

### Time to code!

Setelah mengetahui cara kerja _speech recognition,_ kita akan mencoba untuk membuat **aplikasi untuk mengetahui kondisi cuaca suatu daerah**.

#### Software requirement

*   Python 3
*   Virtual environment
*   [SpeechRecognition](https://pypi.org/project/SpeechRecognition/) Python package
*   [Request](https://pypi.org/project/requests/) Python package

### Time to code!

Data cuaca yang akan digunakan diperoleh dari _weatherstack._ Kita akan mengambil data cuaca saat ini berdasarkan lokasi yang ditentukan. Namun, sebelum menggunakan _weatherstack_ silakan mendaftar untuk mendapatkan _API key_ yang digunakan untuk melakukan _request_ ke _server weatherstack_.

`get_weather_info` merupakan fungsi untuk mendapatkan data yang disediakan oleh [_weatherstack_](https://weatherstack.com/) mengunakan _module request_ yang di-_hit_ ke akses poin _weatherstack._ Jika terjadi _error,_ pesan error tersebut akan dikembalikan sesuai dengan error yang terjadi. Untuk menggunakan API, diperlukan mendaftar ke [_weatherstack_](https://weatherstack.com/) dan menganti _access\_key_ pada _query string_.

Fungsi selanjutnya yang dibuat adalah `speech_to_text_microphone` yang merupakan fungsi untuk _speech recognition_ yang mana suara sumber diambil dari hardware I/O computer. _Package SpeechRecognition_ mendukung banyak _engine_ untuk membuat aplikasi berbasis _Speech recognition._ Salah satunya adalah [Google Cloud Speech API](https://cloud.google.com/speech/) dengan memanfaatkan API yang disediakan oleh Google.

Terakhir adalah menggabungkan kedua fungsi di _main block._ Jika tidak ada kesalaha, akan ditampilkan nama lokasi yang diucapkan dan data cuaca.

Untuk mencoba aplikasi yang telah dibuat, jalankan perinntah untuk melakukan eksekusi file Python. Berikut ini adalah video singkat hasil dari aplikasi yang telah dibuat.

![](https://cdn-images-1.medium.com/max/800/1*-ZKnNwhHZuIXyApkNEETPw.gif)

Keseluruhan kode dapat dilihat di repository yang telah saya buat melalui link berikut ini

[**hellodit/speech-weather**](https://github.com/hellodit/speech-weather)

Original post By [Asdita Prasetya](https://medium.com/@hellodit) on [Medium](https://medium.com/@hellodit/membuat-aplikasi-cuaca-dengan-speech-recognition-482b42aeb341)


