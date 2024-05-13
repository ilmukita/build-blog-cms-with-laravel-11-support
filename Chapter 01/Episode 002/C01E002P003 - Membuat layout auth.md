# C01E002P003 - Membuat layout auth auth

## Layout view

resources\views\layouts\auth\auth-layout.blade.php

```php
<!DOCTYPE html>
<html lang="en">

<head>
   <meta charset="UTF-8">
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   <meta http-equiv="X-UA-Compatible" content="ie=edge">
   <title>Auth Layout</title>
</head>

<body>
   @yield('content')
</body>

</html>
```

## Controller Login

```bash
php artisan make:controller Auth/LoginController
```

app\Http\Controllers\Auth\LoginController.php

```php
<?php

namespace App\Http\Controllers\Auth;

use App\Http\Controllers\Controller;
use Illuminate\Http\Request;

class LoginController extends Controller
{
    public function index()
    {
        return view("auth.login.index");
    }
}
```

resources\views\auth\login\index.blade.php

```php
@extends('layouts.auth.auth-layout')

@section('content')
   Login Page
@endsection
```

## Route

```php
Route::get('/login', [App\Http\Controllers\Auth\LoginController::class, 'index'])->name('auth.login');
```


