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

![img29](/img/imgpraktikum11.29.png)

## Instalasi Codeigniter 4
Untuk melakukan instalasi Codeigniter 4 dapat dilakukan dengan dua cara, yaitu cara manual dan menggunakan composer. Pada praktikum ini kita menggunakan cara manual.

- Unduh Codeigniter dari website https://codeigniter.com/download
- Extrak file zip Codeigniter ke direktori htdocs/lab11_ci.
- Ubah nama direktory framework-4.x.xx menjadi ci4.
- Buka browser dengan alamat http://localhost/lab11_ci/ci4/public/

![img28](/img/imgpraktikum11.28.png)

## Menjalankan CLI (Command Line Interface)
Codeigniter 4 menyediakan CLI untuk mempermudah proses development. Untuk mengakses CLI buka terminal/command prompt.

![img30](/img/imgpraktikum11.30.png)

Arahkan lokasi direktori sesuai dengan direktori kerja project dibuat
```(xampp/htdocs/lab11_ci/ci4/).```
Perintah yang dapat dijalankan untuk memanggil CLI Codeigniter adalah :
```php spark```
![img32](/img/imgpraktikum11.32.png)

## Mengaktifkan Mode Debugging
- Ketik ```php spark serve``` pada CLI untuk menjalankan.
![img33](/img/imgpraktikum11.33.png)

- Menampilkan pesan error, untuk mencobanya ubah kode file app/Controllers/home.php, hapus ;nya.
![img8](/img/imgpraktikum11.8.png)

- Ketik ```http://localhost:8080``` pada browser. Berikut tampilan error nya.
![img34](/img/imgpraktikum11.34.png)

- Kemudian, ubah nama file ```env``` menjadi ```.env```. Masuk ke dalam filenya, hapus tanda ```#``` pada ```CI_ENVIRONMENT``` =
![img35](/img/imgpraktikum11.35.png)
- Refresh url sebelumnya, Berikut tampilan error nya.
![img36](/img/imgpraktikum11.36.png)


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

```php spark routes```
![img13](/img/imgpraktikum11.13.png)

Selanjutnya coba akses route yang telah dibuat dengan mengakses alamat url http://localhost:8080/about
![img37](/img/imgpraktikum11.37.png)


## Membuat Controller
Selanjutnya adalah membuat Controller Page. Buat file baru dengan nama ```page.php``` pada direktori Controller kemudian isi kodenya seperti berikut.
![img14](/img/imgpraktikum11.14.png)

Selanjutnya refresh Kembali browser, maka akan ditampilkan hasilnya yaitu halaman sudah dapat diakses.
![img15](/img/imgpraktikum11.15.png)

- Auto Routing Secara default fitur autoroute pada Codeiginiter sudah aktif. Untuk mengubah status autoroute dapat mengubah nilai variabelnya. Untuk menonaktifkan ubah nilai `true` menjadi `false`.

`$routes->setAutoRoute(true);`
![img16](/img/imgpraktikum11.16.png)

Tambahkan method baru pada Controller Page seperti berikut.
```php
public function tos()
{
    echo "ini halaman Term of Services";
}
```
![img17](/img/imgpraktikum11.17.png)

Method ini belum ada pada routing, sehingga cara mengaksesnya dengan menggunakan alamat: http://localhost:8080/page/tos
![img18](/img/imgpraktikum11.18.png)

## Membuat View
Selanjutnya adalam membuat view untuk tampilan web agar lebih menarik. Buat file baru dengan nama about.php pada direktori view ```(app/Views/about.php)``` kemudian isi kodenya seperti berikut.
```php
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <title><?= $title; ?></title>
    </head>
    <body>
        <h1><?= $title; ?></h1>
        <hr>
        <p><?= $content; ?></p>
    </body>
</html>
```
![img19](/img/imgpraktikum11.19.png)

Ubah ```method about``` pada class ```Controller Page``` menjadi seperti berikut:
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
Buat file css pada direktori ```public``` dengan nama ```style.css``` (copy file dari praktikum lab4_layout. Kita akan gunakan layout yang pernah dibuat pada praktikum 4.
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
![img22](/img/imgpraktikum11.22.png)
Kemudian buat folder template pada direktori view kemudian buat file ```header.php``` dan ```footer.php```
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
File app/view/template/header.php
![img38](/img/imgpraktikum11.38.png)

File app/view/template/footer.php
![img39](/img/imgpraktikum11.39.png)

Kemudian ubah file ```app/view/about.php``` seperti berikut.
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

- Pada ```Controllers/page.php```, menjadi berikut
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
- Pada masing-masing file di dalam Views, buat file baru denga nama : `rumah.php`,`about.php`,`artikel.php`,`contact.php`,`faqs.php`, dan `tos.php`. Masukan kode dibawah ini ke semua file tersebut
```php
    <?= $this->include('template/header'); ?>
    <h1><?= $title; ?></h1>
    <hr>
    <p><?= $content; ?></p>
    <?= $this->include('template/footer'); ?>
```
![img40](/img/imgpraktikum11.40.png)

### Praktikum 12 | Framework Lanjutan (CRUD)
# 1. Database
- Jalankan Apache, MySql pada Xampp, Buat database dengan nama lab_ci4 di http://localhost/phpmyadmin.
- Buat tabel dengan nama artikel.
```php
CREATE TABLE artikel (
    id INT(11) auto_increment,
    judul VARCHAR(200) NOT NULL,
    isi TEXT,
    gambar VARCHAR(200),
    status TINYINT(1) DEFAULT 0,
    slug VARCHAR(200),
    PRIMARY KEY(id)
);
```
![img46](/img/imgpraktikum11.46.png)

# 2. Konfigurasi Koneksi Database
- Terletak di folder `ci4`, file `.env`, Hapus tanda `#`.
![img42](/img/imgpraktikum11.42.png)

# 3. Membuat Model
- Terletak di folder `app/Models`, buat file `ArtikelModel.php`.
![img43](/img/imgpraktikum11.43.png)

# 4. Membuat Controller
- Terletak di folder `app/Controllers`, buat file `Artikel.php`.
```php
<?php
namespace App\Controllers;
use App\Models\ArtikelModel;
class Artikel extends BaseController
{
    public function index()
    {
        $title = 'Daftar Artikel';
        $model = new ArtikelModel();
        $artikel = $model->findAll();
        return view('artikel/index', compact('artikel', 'title'));
    }
}
```
![img44](/img/imgpraktikum11.44.png)

# 5. Membuat View pada artikel
- Terletak di folder `app/Views/artikel`, buat file `index.php`.
![img45](/img/imgpraktikum11.45.png)

- Buka browser, ketik http://localhost:8080/artikel 
![img47](/img/imgpraktikum11.47.png)

- Masukkan data ke tabel artikel
INSERT INTO artikel (judul, isi, slug) VALUE
('Artikel pertama', 'Lorem Ipsum adalah contoh teks atau dummy dalam industri 
percetakan dan penataan huruf atau typesetting. Lorem Ipsum telah menjadi 
standar contoh teks sejak tahun 1500an, saat seorang tukang cetak yang tidak 
dikenal mengambil sebuah kumpulan teks dan mengacaknya untuk menjadi sebuah 
buku contoh huruf.', 'artikel-pertama'), 
('Artikel kedua', 'Tidak seperti anggapan banyak orang, Lorem Ipsum bukanlah 
teks-teks yang diacak. Ia berakar dari sebuah naskah sastra latin klasik dari 
era 45 sebelum masehi, hingga bisa dipastikan usianya telah mencapai lebih 
dari 2000 tahun.', 'artikel-kedua');
![img48](/img/imgpraktikum11.48.png)

# 6. Membuat Tampilan detail Artikel
- Terletak di folder `app/Controllers`, edit file `Artikel.php`. Tambah method view().
![img49](/img/imgpraktikum11.49.png)

7. Membuat View pada Detail
- Terletak di folder `app/Views/artikel`, buat file `detail.php`.
![img50](/img/imgpraktikum11.50.png)

8. Membuat Routing untuk artikel detail
- Terletak di folder `app/Config`, edit file `Routes.php`.
![img51](/img/imgpraktikum11.51.png)

- Klik `Artikel Kedua` pada http://localhost:8080/artikel, untuk pindah ke detailnya.
![img52](/img/imgpraktikum11.52.png)

9. Membuat Menu admin
- Terletak di folder `app/Controller`, edit file `Artikel.php`. Tambah method `admin_index()`.
![img53](/img/imgpraktikum11.53.png)

- Selanjutnya, akses kembali folder `app/Views/artikel`, buat file `admin_index.php`.
```php
<?= $this->include('template/admin_header'); ?>
<table class="table table-bordered table-hover">
    <thead>
        <tr class="table-primary">
            <th scope="col">ID</th>
            <th scope="col">Judul</th>
            <th scope="col">Status</th>
            <th scope="col">Aksi</th>
        </tr>
    </thead>
    <tbody>
        <?php if($artikel): foreach($artikel as $row): ?>
        <tr>
            <td><?= $row['id']; ?></td>
            <td>
                <b><?= $row['judul']; ?></b>
                <p><small><?= substr($row['isi'], 0, 50); ?></small></p>
            </td>
            <td><?= $row['status']; ?></td>
            <td>
                <a class="btn btn-primary p-1" href="<?= base_url('/admin/artikel/edit/' . 
                $row['id']);?>">Ubah</a>
                <a class="btn btn-danger p-1" onclick="return confirm('Yakin menghapus data?');" href="<?= base_url('/admin/artikel/delete/' . 
                $row['id']);?>">Hapus</a>
            </td>
        </tr>
        <?php endforeach; else: ?>
        <tr>
            <td colspan="4">Belum ada data.</td>
        </tr>
        <?php endif; ?>
    </tbody>
    <tfoot>
        <tr class="table-primary">
            <th scope="col">ID</th>
            <th scope="col">Judul</th>
            <th scope="col">Status</th>
            <th scope="col">Aksi</th>
        </tr>
    </tfoot>
</table>
<?= $this->include('template/admin_footer'); ?>
```
- Buka folder yang ada di `app/Views/artikel/template`, kemudian buat:
`admin_header.php`
![img54](/img/imgpraktikum11.54.png)

- `admin_footer.php`
![img55](/img/imgpraktikum11.55.png)

# 10. Membuat Routing untuk menu admin
- Terletak di folder `app/Config`, edit file `Routes.php`.
![img56](/img/imgpraktikum11.56.png)

- Akses browser dengan http://localhost:8080/admin/artikel.

![img57](/img/imgpraktikum11.57.png)

# 11. Menambah data untuk Artikel
- Terletak di folder `app/Controller`, edit file `Artikel.php`. Tambah method `add()`.
![img58](/img/imgpraktikum11.58.png)

- Akses kembali folder `app/Views/artikel`, buat file `form_add.php`.
![img59](/img/imgpraktikum11.59.png)

- Akses browser dengan http://localhost:8080/admin/artikel/add.
![img60](/img/imgpraktikum11.60.png)

# 12.  Mengubah data pada Artikel
- Terletak di folder `app/Controller`, edit file `Artikel.php`. Tambah method `edit()`.
![img61](/img/imgpraktikum11.61.png)

- Akses kembali folder `app/Views/artikel`, buat file `form_edit.php`.
![img62](/img/imgpraktikum11.62.png)

- Akses browser dengan http://localhost:8080/admin/artikel/edit/1 untuk Mengubah artikel pertama.
![img63](/img/imgpraktikum11.63.png)

# 13. Menghapus data pada Artikel
- Terletak di folder app/Controller, edit file Artikel.php. Tambah method delete().
![img64](/img/imgpraktikum11.64.png)

- Akses browser dengan http://localhost:8080/admin/artikel/add untuk membuat artikel ketiga, lalu kirim.
![img65](/img/imgpraktikum11.65.png)

- Pergi ke menu admin untuk menghapusnya, http://localhost:8080/admin/artikel, kemudian pilih hapus.
![img66](/img/imgpraktikum11.66.png)

- Artikel berhasil dihapus.
![img67](/img/imgpraktikum11.67.png)













































