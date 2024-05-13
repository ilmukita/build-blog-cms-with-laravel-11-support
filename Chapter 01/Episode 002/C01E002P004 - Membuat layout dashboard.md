# C01E002P004 - Membuat layout dashboard

## Layout view

resources\views\layouts\dashboard\dashboard-layout.blade.php

```php
<!DOCTYPE html>
<html lang="en">

<head>
   <meta charset="UTF-8">
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   <meta http-equiv="X-UA-Compatible" content="ie=edge">
   <title>Dashboard Layout</title>
</head>

<body>
   @yield('content')
</body>

</html>
```

## Controller Home

```bash
php artisan make:controller Dashboard/HomeController
```

app\Http\Controllers\Dashboard\HomeController.php

```php
<?php

namespace App\Http\Controllers\Dashboard;

use App\Http\Controllers\Controller;
use Illuminate\Http\Request;

class HomeController extends Controller
{
    public function index()
    {
        return view("dashboard.home.index");
    }
}
```

resources\views\dashboard\home\index.blade.php

```php
@extends('layouts.dashboard.dashboard-layout')

@section('content')
   Dashboard Page
@endsection
```

## Route

```php
Route::get('/dashboard', [App\Http\Controllers\Dashboard\HomeController::class, 'index'])->name('dashboard.login');
```


