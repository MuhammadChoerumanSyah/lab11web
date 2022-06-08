| Nama      | Muhammad Choeruman Syah |
| ----------- | ----------- |
| NIM     | 312010031       |
| Kelas   | TI.20.A.1        |

## Langkah langkah praktikum
## Persiapan
Sebelum memulai menggunakan Framework Codeigniter, perlu dilakukan konfigurasi pada webserver. Beberapa ekstensi PHP perlu diaktifkan untuk kebutuhan pengembangan Codeigniter 4. Berikut beberapa ekstensi yang perlu diaktifkan:
- php-json ekstension untuk bekerja dengan JSON;
- php-mysqlnd native driver untuk MySQL;
- php-xml ekstension untuk bekerja dengan XML;
- php-intl ekstensi untuk membuat aplikasi multibahasa;
- libcurl (opsional), jika ingin pakai Curl.

Untuk mengaktifkan ekstentsi tersebut, melalu XAMPP Control Panel, pada bagian Apache klik ```Config -> PHP.ini```

![img1](/img/imgpraktikum11.1.png)

Pada bagian extention, hilangkan tanda ; (titik koma) pada ekstensi yang akan
diaktifkan. Kemudian simpan kembali filenya dan restart Apache web server.

![img2](/img/imgpraktikum11.2.png)

## Instalasi Codeigniter 4
Untuk melakukan instalasi Codeigniter 4 dapat dilakukan dengan dua cara, yaitu cara manual dan menggunakan composer. Pada praktikum ini kita menggunakan cara manual.

- Unduh Codeigniter dari website https://codeigniter.com/download
- Extrak file zip Codeigniter ke direktori htdocs/lab11_ci.
- Ubah nama direktory framework-4.x.xx menjadi ci4.
- Buka browser dengan alamat http://localhost/lab11_ci/ci4/public/

![img3](/img/imgpraktikum11.3.png)

## Menjalankan CLI (Command Line Interface)
Codeigniter 4 menyediakan CLI untuk mempermudah proses development. Untuk mengakses CLI buka terminal/command prompt.

![img4](/img/imgpraktikum11.4.png)

Arahkan lokasi direktori sesuai dengan direktori kerja project dibuat
```(xampp/htdocs/lab11_ci/ci4/).```
Perintah yang dapat dijalankan untuk memanggil CLI Codeigniter adalah :
```php spark```
![img5](/img/imgpraktikum11.5.png)
![img6](/img/imgpraktikum11.6.png)

## Mengaktifkan Mode Debugging
- Ketik ```php spark serve``` pada CLI untuk menjalankan.
![img7](/img/imgpraktikum11.7.png)

- Menampilkan pesan error, untuk mencobanya ubah kode file app/Controllers/home.php, hapus ;nya.
![img8](/img/imgpraktikum11.8.png)

- Ketik ```http://localhost:8080``` pada browser. Berikut tampilan error nya.
![img9](/img/imgpraktikum11.9.png)

- Kemudian, ubah nama file ```env``` menjadi ```.env```. Masuk ke dalam filenya, hapus tanda ```#``` pada ```CI_ENVIRONMENT``` =
![img10](/img/imgpraktikum11.10.png)

## Struktur Direktori
![img11](/img/imgpraktikum11.11.png)

## Routing and Controller
Router terletak pada file ```app/config/Routes.php```

## Membuat Route Baru
Tambahkan kode berikut di dalam ```Routes.php```
```php
$routes->get('/about', 'Page::about');
$routes->get('/contact', 'Page::contact');
$routes->get('/faqs', 'Page::faqs');
```


![img12](/img/imgpraktikum11.12.png)

## Untuk mengetahui route yang ditambahkan sudah benar, buka CLI dan jalankan perintah berikut.

php spark routes
![img13](/img/imgpraktikum11.13.png)

Selanjutnya coba akses route yang telah dibuat dengan mengakses alamat url http://localhost:8080/about

## Membuat Controller
Selanjutnya adalah membuat Controller Page. Buat file baru dengan nama ```page.php``` pada direktori Controller kemudian isi kodenya seperti berikut.
![img14](/img/imgpraktikum11.14.png)

Selanjutnya refresh Kembali browser, maka akan ditampilkan hasilnya yaitu halaman sudah dapat diakses.
![img15](/img/imgpraktikum11.15.png)

- Auto Routing Secara default fitur autoroute pada Codeiginiter sudah aktif. Untuk mengubah status autoroute dapat mengubah nilai variabelnya. Untuk menonaktifkan ubah nilai `true` menjadi `false`.

`$routes->setAutoRoute(true);`
![img16](/img/imgpraktikum11.16.png)

Tambahkan method baru pada Controller Page seperti berikut.

public function tos()
{
    echo "ini halaman Term of Services";
}
![img17](/img/imgpraktikum11.17.png)

Method ini belum ada pada routing, sehingga cara mengaksesnya dengan menggunakan alamat: http://localhost:8080/page/tos
![img18](/img/imgpraktikum11.18.png)

## Membuat View
Selanjutnya adalam membuat view untuk tampilan web agar lebih menarik. Buat file baru dengan nama about.php pada direktori view (app/Views/about.php) kemudian isi kodenya seperti berikut.
![img19](/img/imgpraktikum11.19.png)

Ubah method about pada class Controller Page menjadi seperti berikut:
```php
public function about()
{
    return view('about', [
        'title' => 'Halaman About',
        'content' => 'Ini adalah halaman abaut yang menjelaskan tentang isi halaman ini.'
        ]);
}
```

![img20](/img/imgpraktikum11.20.png)

Kemudian lakukan refresh pada halaman tersebut.
![img21](/img/imgpraktikum11.21.png)

## Membuat Layout Web dengan CSS
Buat file css pada direktori public dengan nama style.css (copy file dari praktikum lab4_layout. Kita akan gunakan layout yang pernah dibuat pada praktikum 4.
![img22](/img/imgpraktikum11.22.png)
```css
/* import google font */
@import
url('https://fonts.googleapis.com/css2?family=Open+Sans:ital,wght@0,300;0,400 ;0,600;0,700;0,800;1,300;1,400;1,600;1,700;1,800&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Open+Sans+Condensed:ital,wght@0 ,300;0,700;1,300&display=swap');
/* Reset CSS */
*{
	margin: 0;
	padding: 0; 
}
body{ 
	line-height:1;
	font-size:100%;
	font-family:'Open Sans', sans-serif; 
	color:#5a5a5a;
}
#container{
    width: 980px;
    margin: 0 auto;
	box-shadow: 0 0 1em #cccccc; 
}

/* header */
header{
    padding: 20px;
}
header h1{
    margin: 20px 10px;
    color: #b5b5b5;
}

/* navigasi */
nav{
    display: block;
	background-color: #1f5faa; 
}
nav a {
	padding: 15px 30px; 
	display: inline-block; 
	color: #ffffff; 
	font-size: 14px; 
	text-decoration: none; 
	font-weight: bold;
}
nav a.active, 
nav a:hover{
	background-color: #2b83ea; 
}

/* Hero Panel */
#hero{
	background-color: #e4e4e5; 
	padding: 50px 20px; 
	margin-bottom: 20px;
}
#hero h1{ 
	margin-bottom: 20px; 
	font-size: 35px;
}
#hero p{ 
	margin-bottom: 20px; 
	font-size: 18px; 
	line-height: 25px;
}

/* main content */
#wrapper {
    margin: 0;
}
#main {
    float: left;
    width: 640px;
    padding: 20px;
}
/* sidebar area */
#sidebar {
    float: left;
    width: 260px;
    padding: 20px;
}

/* widget */
.widget-box{
border:1px solid #eee; 
margin-bottom:20px;
}
.widget-box 
.title{ 
	padding:10px 16px; 
	background-color:#428bca; 
	color:#fff;
}
.widget-box ul{ 
	list-style-type:none;
}
.widget-box li{ 
	border-bottom:1px solid #eee;
}
.widget-box li a{ 
	padding:10px 16px; 
	color:#333; 
	display:block; 
	text-decoration:none;
}
.widget-box 
li:hover a{ 
	background-color:#eee;
}
.widget-box p{ 
	padding:15px;
	line-height:25px; 
}

/* footer */
footer {
    clear:both;
	background-color:#1d1d1d; 
	padding:20px;
	color:#eee;
}

/* layout About */
.about{
	display: flex;
	align-items: center;
	justify-content: space-between;
	background-color: #e4e4e5; 
	clear: both;
	padding:35px;
	line-height:25px; 
}

.avatar {
  width: 110px;
  border-radius: 50%;
}

/* Layout Kontak */
.kontak-body {
    margin: 0;
    font-family: -apple-system, Arial, sans-serif;
    font-size: 1rem;
    font-weight: 400;
    line-height: 1.5;
    text-align: left;
    padding: 30px;
    padding-bottom: 10px;
    border: 1px solid #ced4da;
    border-radius: 0.25rem;
    max-width: 100%;
}
.kontak-form-group {
    margin-bottom: 1rem;
}

.kontak-input-group {
    position: relative;
    display: -ms-flexbox;
    display: flex;
    -ms-flex-wrap: wrap;
    flex-wrap: wrap;
    -ms-flex-align: stretch;
    align-items: stretch;
    width: 100%;
}

.kontak-form-control {
    display: block;
    width: 100%;
    height: calc(1.5em + 0.75rem + 2px);
    padding: 0.375rem 0.75rem;
    font-size: 1rem;
    font-weight: 400;
    line-height: 1.5;
    color: #495057;
    background-color: #fff;
    background-clip: padding-box;
    border: 1px solid #ced4da;
    outline: none;
    border-radius: 0.25rem;
    transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
}

.kontak-form-control:focus {
    border: 1px solid #313131;
}


textarea.kontak-form-control {
    height: auto;
}

label.kontak-label {
    display: inline-block;
    margin-bottom: 0.5rem;
}


.kontak-btn {
    display: inline-block;
    font-weight: 400;
    color: #212529;
    text-align: center;
    vertical-align: middle;
    cursor: pointer;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    background-color: transparent;
    border: 1px solid transparent;
    padding: 0.375rem 0.75rem;
    font-size: 1rem;
    line-height: 1.5;
    border-radius: 0.25rem;
    transition: color 0.15s ease-in-out, background-color 0.15s ease-in-out, border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
}

.kontak-btn-primary {
    color: #fff;
    background-color: #007bff;
    border-color: #007bff;
}

.kontak-btn-lg, 
.kontak-btn-group-lg>
.kontak-btn {
    padding: 0.5rem 1rem;
    font-size: 1.25rem;
    line-height: 1.5;
    border-radius: 0.3rem;
}


input[type="submit"].kontak-btn-block, 
input[type="reset"].kontak-btn-block, 
input[type="button"].kontak-btn-block {
    width: 100%;
}

/* box */
.box { 
	display:block;
	float:left;
	width:33.333333%; 
	box-sizing:border-box; 
	-moz-box-sizing:border-box; 
	-webkit-box-sizing:border-box;
	padding:0 10px;
	text-align:center; 
}
.box h3 {
	margin: 15px 0;
}
.box p {
	line-height: 20px; 
	font-size: 14px; 
	margin-bottom: 15px;
}
box img {
	border: 0;
	vertical-align: middle; 
}
.image-circle { 
	border-radius: 50%;
}
.row {
	margin: 0 -10px;
	box-sizing: border-box; 
	-moz-box-sizing: border-box; 
	-webkit-box-sizing: border-box;
}
.row:after, 
.row:before, 
.entry:after, 
.entry:before {
	content:'';
    display:table;
}
.row:after, 
.entry:after {
    clear:both;
}

.divider { border:0;
border-top:1px solid #eeeeee;
    margin:40px 0;
}

/* entry */
.entry {
	margin: 15px 0;
}
.entry h2 { 
	margin-bottom: 20px;
}
.entry p { 
	line-height: 25px;
}
.entry img { 
	float: left;
	border-radius: 5px;
	margin-right: 15px; 
}
.entry .right-img { 
	float: right;
}
```

Kemudian buat folder template pada direktori view kemudian buat file header.php dan footer.php
```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title><?= $title; ?></title>
    <link rel="stylesheet" href="<?= base_url('/style.css');?>">
</head>
<body>
    <div id="container">
        <header>
            <h1>Layout Sederhana</h1>
        </header>
        <nav>
            <a href="<?= base_url('/');?>" class="active">Home</a>
            <a href="<?= base_url('/artikel');?>">Artikel</a>
            <a href="<?= base_url('/about');?>">About</a>
            <a href="<?= base_url('/contact');?>">Kontak</a>
        </nav>
        <section id="wrapper">
            <section id="main">
```
![img23](/img/imgpraktikum11.23.png)

File app/view/template/footer.php 
![img24](/img/imgpraktikum11.24.png)

Kemudian ubah file app/view/about.php seperti berikut.

```php
<?= $this->include('template/header'); ?>
<h1><?= $title; ?></h1>
<hr>
<p><?= $content; ?></p>
<?= $this->include('template/footer'); ?>
```
![img25](/img/imgpraktikum11.25.png)

Selanjutnya refresh tampilan pada alamat http://localhost:8080/about
![img26](/img/imgpraktikum11.26.png)

## Pertanyaan dan Tugas
Lengkapi kode program untuk menu lainnya yang ada pada Controller Page, sehingga semua link pada navigasi header dapat menampilkan tampilan dengan layout yang sama.

## Jawaban
- Ubah isi pada Routes.php menjadi berikut,
![img27](/img/imgpraktikum11.27.png)

- Pada Controllers/page.php, menjadi berikut
```php
<?php
namespace App\Controllers;

class Page extends BaseController
{
    public function rumah()
    {
        return view('rumah', [
        'title' => 'Halaman Home',
        'content' => 'Ini adalah halaman home yang menjelaskan tentang isi
        halaman ini.'
        ]);
    }

    public function about()
    {
        return view('about', [
        'title' => 'Halaman About',
        'content' => 'Ini adalah halaman about yang menjelaskan tentang isi 
        halaman ini.'
        ]);
    }

    public function contact()
    {
        return view('contact', [
        'title' => 'Halaman Contact',
        'content' => 'Ini adalah halaman contact yang menjelaskan tentang isi 
        halaman ini.'
        ]);
    }

    public function artikel()
    {
        return view('artikel', [
        'title' => 'Halaman Artikel',
        'content' => 'Ini adalah halaman artikel yang menjelaskan tentang isi 
        halaman ini.'
        ]);
    }

    public function faqs()
    {
        return view('faqs', [
            'title' => 'Halaman FAQ',
            'content' => 'Ini adalah halaman FAQ yang menjelaskan tentang isi 
            halaman ini.'
            ]);
    }

    public function tos()
    {
        return view('tos', [
        'title' => 'Halaman TOS',
        'content' => 'Ini adalah halaman Terms of Service yang menjelaskan tentang isi 
        halaman ini.'
        ]);
    }
}
```


































