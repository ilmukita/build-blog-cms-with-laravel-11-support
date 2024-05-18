# C01E004P007 - Menambahkan Middleware Auth dan Guest

routes\web.php

```php
Route::middleware(['guest'])->group(function () {
   // route list
});

Route::middleware(['auth'])->group(function () {
   // route list
});
```

## Ikhtisar

Dalam Laravel, middleware `auth` dan `guest` digunakan untuk kontrol akses terhadap route (halaman) di aplikasi Anda. Keduanya memiliki fungsi yang berlawanan:

**Middleware `auth`** digunakan untuk **membatasi akses** ke route tertentu hanya untuk pengguna yang sudah **terlogin**.

- Jika pengguna sudah login, middleware `auth` akan memperbolehkan akses ke route tersebut.
- Jika pengguna belum login, middleware `auth` akan memblokir akses dan biasanya akan mengalihkan pengguna ke halaman login atau menampilkan pesan error.

**Middleware `guest`** digunakan untuk **membatasi akses** ke route tertentu hanya untuk pengguna yang **belum login**.

- Jika pengguna belum login, middleware `guest` akan memperbolehkan akses ke route tersebut.
- Jika pengguna sudah login, middleware `guest` akan memblokir akses dan biasanya akan mengalihkan pengguna ke halaman dashboard atau halaman lain yang ditujukan untuk pengguna yang sudah login.

Ringkasan Perbedaan:

| Fitur                         | Middleware auth                | Middleware guest                      |
| ----------------------------- | ------------------------------ | ------------------------------------- |
| Pengguna yang bisa mengakses  | Telah login                    | Belum login                           |
| Fungsi                        | Membatasi akses                | Membatasi akses                       |
| Tindakan jika terpenuhi       | Izinkan akses                  | Izinkan akses                         |
| Tindakan jika tidak terpenuhi | Blokir akses, alihkan ke login | Blokir akses, alihkan ke halaman lain |

## Ref

- https://laravel.com/docs/11.x/middleware
