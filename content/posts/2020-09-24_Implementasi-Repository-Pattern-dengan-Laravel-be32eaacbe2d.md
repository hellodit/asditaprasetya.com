---
title: Implementasi Repository Pattern dengan Laravel
tags:
  - Design Pattern
  - Software Engineering
categories: 
  - Software Architecture
date: 2020-09-24T08:43:26+07:00
draft: false
description: Singkatnya Repository Pattern adalah suatu pendekatan yang memisahkan antara Business Logic layer dengan Data Access Logic layer.
---

Singkatnya Repository Pattern adalah suatu pendekatan yang memisahkan antara Business Logic layer dengan Data Access Logic layer.

![](https://cdn-images-1.medium.com/max/800/1*m4ziWIbBLR-Mmq4v-1KSig.jpeg)

_Design pattern_ adalah suatu metode yang digunakan untuk menyelesaikan permasalahan yang berulang dan biasanya memiliki suatu pola dalam menyelesaikan masalah. _Design Pattern_ dapat mempercepat pengembangan suatu perangkat lunak. Salah satu dari _Design Pattern_ yang paling sering digunakan adalah _Repository Pattern_.

### What is Repository Pattern?

Secara singkatnya **_Repository Pattern_** adalah suatu pendekatan yang memisahkan antara Business Logic layer dengan _Data Access Logic layer._

Menggunakan _repository pattern_, business logic layer tidak harus tahu dari mana sumber data diambil atau ke mana data akan dikirim. Business logic layer hanya bertugas untuk melakukan implementasi proses bisnis yang ingin diselesaikan atau masalah yang seharusnya diselesaikan.

![](https://cdn-images-1.medium.com/max/800/1*Q1o9gDS7V5eB7VPqRKEDvw.png)

Proses yang berhubungan dengan pengambilan atau pengiriman data nantinya akan ditangani oleh _Data Access Logic layer,_ yang mana juga bertugas untuk melakukan abstraksi _query._ Tujuannya untuk mengurangi kompleksitas dan memberikan keuntungan dalam _reusability_ ketika harus menangani _query_ yang kompleks.

Untuk memahami cara kerja **Repository Pattern,** dapat membuka link [**martinfowler**](https://martinfowler.com/eaaCatalog/repository.html).

#### **_Single Responsibility Principle_**

Pendekatan ini sesuai dengan kaidah _Single Responsibility Principle_ pada [**SOLID**](https://en.wikipedia.org/wiki/SOLID)**.** yang artinya setiap _class_ atau fungsi haruslah memiliki satu tanggung jawab saja. Contoh ada _class_ untuk mendefinisikan struktur data dan ada _class_ untuk melakukan manipulasi data.

Suatu _class_ atau fungsi **tidak diperbolehkan** untuk menjadi fungsi atau _class_ yang **_palugada_** atau _class_ yang mengerjakan banyak hal. Dalam suatu _class method_ dan _property_ harus bekerja sama untuk mengerjakan atau memecahkan satu permasalahan saja.

### Implementasi Repository Pattern

Kali ini saya akan melakukan implementasi _Repository Pattern_ dengan menggunakan Laravel versi 8. _Project_ yang akan kita buat kali ini adalah **aplikasi Todo list berbasis Restful API.** Jika belum mengetahui apa itu _Restfull API,_ dapat membaca terlebih dahulu artikel berikut.

**What is REST** 
[REST is acronym for REpresentational State Transfer. It is architectural style for distributed hypermedia systems and…](https://restfulapi.net)

### Aplikasi Todo list berbasis Restful API

#### **Fitur Utama**

1.  Pengguna dapat melakukan CRUD _Task._
2.  Pengguna dapat menandai _task_ yang sudah selesai dikerjakan.
3.  Pengguna dapat menuliskan komentar di _task_ yang telah dibuat.

#### **Rancangan Database**

![](https://cdn-images-1.medium.com/max/800/1*6S8K8Px4NBPGOcLEiLF2aA.png)

#### **_Time to code_**

Buatlah _project_ Laravel baru dengan versi Laravel sesuai keinginan, saya sarankan untuk menggunakan Laravel versi 5 ke atas. Buatlah migrasi, model dan _controller_ untuk tabel _task_, untuk mempermudah dapat menggunakan command di bawah ini:

```
php artisan make:model -mc
```

Jika berhasil, akan ada 3 file baru yaitu file model, _migration_ dan _controller_. Buatlah file migrasi sesuai diagram tabel yang ada di atas atau dapat menggunakan fungsi berikut.

```php
public function up()    
{        
    Schema::create('tasks', function (Blueprint $table)
    {            
        $table->id();            
        $table->string('name', 150);            
        $table->text('description')->nullable();            
        $table->boolean('status')->default(false);            
        $table->timestamps();        
    });    
}
```

Langkah selanjutnya adalah buka folder “app” lalu buat folder bernama “_Repository_”. Folder ini akan menyimpan berbagai _repository_ yang akan digunakan. Setelah itu buat folder “_Task_” di dalam folder “_Repository_”, folder ini akan menyimpan seluruh Repository yang berhubungan dengan _Task_. Jika dilihat maka struktur folder “app” akan menjadi seperti ini.

```
app
├───Console
├───Exceptions
├───Http
│   ├───Controllers
│   └───Middleware
├───Models
├───Providers
├───Repository --> Folder untuk menyimpan Repository
│   └───Task
└───Utils
```

#### **Membuat Interface Repository**

Untuk melakukan proses **_code-decoupling_** maka dibuat **_interface_** yang nantinya akan diimplementasi oleh kelas yang berhubungan dengan fitur yang ingin menggunakan _repository pattern_.

_Interface_ menjadi kontrak bagi _child class-nya_ sehingga memberikan keleluasaan dalam pemilihan mekanisme _Data Access Logic._ Misal menggunakan Eloquent maka buat kelas “**EloquentTaskRepositoy**” sebagai _child_ dari “**TaskRepository**”, atau menggunakan Elasticsearch maka dapat membuat _class_ dengan **ElasticsearchTaskRepository** sebagai _child_ dari “**TaskRepository**”. Pada implementasi kali ini akan menggunakan Eloquent sebagai _data access logic._ Pada folder “Task” buat 2 file yaitu **TaskRepository.php** dan **EloquentTaskRepositoy.php.**

```php 
//interface TaskRepository TaskRepository.php
namespace App\\Repository\\Task;
interface TaskRepository
{
    public function createTask(Request $request);
    public function getTasks();
    public function getTasksById($id);
    public function updateTask(Request $request, $id);
    public function setAsFinish($id);
}
//EloquentTaskRepositoy EloquentTaskRepositoy.php. 
class EloquentTaskRepository implements TaskRepository
{
...
    public function updateTask(Request $request, $id)
    {
       $task = Task::whereId($id)->first();
        if ($task != null) {
            $task->update([
                'name' => $request->name,
                'description' => $request->description,
            ]);
            return $task;
        }
        return null;
    }
...
}
```

Kita berhasil menambahkan layer baru menggunakan _Repository Pattern._ Langkah terakhir adalah dengan implementasi di _controller_.

```php 
use App\Repository\Task\EloquentTaskRepository;
use App\Utils\Response;
class TaskController extends Controller
{
    use Response;
    protected $eloquentTask;
    public function __construct(EloquentTaskRepository $eloquentTask) {
        $this->eloquentTask = $eloquentTask;
    }
    public function tasks(){
        $tasks = $this->eloquentTask->getTasks();
        if (!$tasks->isEmpty()){
            return $this->responseDataCount($tasks);
        }
        return $this->responseDataNotFound('Data yang diminta tidak tersedia');
    }
    public function getTasksById($id){
        $task = $this->eloquentTask->getTasksById($id);
        if (!empty($task)){
            return $this->responseData($task);
        }
        return $this->responseDataNotFound('Data yang diminta tidak tersedia');
    }
}
```

Menggunakan objek dari “**EloquentTaskRepository”,** _controller_ dapat fokus hanya untuk menulis Business logic, _query_ akses database yang panjang dan rumit sudah di enkapsulasi pada “**EloquentTaskRepository**”. Sampai sini implementasi _Repository Pattern_ telah selesai.

Source code dapat diakses melalui [Github](https://github.com/hellodit/laravel-repository-pattern).

### Kesimpulan

*   Dengan mengunakan _Repository Pattern_, dapat memisahkan antara _business logic_ dan _data access logic_. _Repository Pattern_ akan melakukan abstraksi terhadap _data access logic_.
*   Dengan implementasi _Repository Pattern_, pengembangan perangkat lunak akan sesuai dengan kaidah SOLID.
*   _Repository Pattern_ dapat mempermudah dalam proses pengembangan perangkat lunak.
*   _Repository Pattern_ dapat diimplementasi pada berbagai macam bahasa pemrograman.
