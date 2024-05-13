

# Membuat layout utama



## View layout

resources\views\layouts\site\site-layout.blade.php

```php
<!DOCTYPE html>
<html lang="en">

<head>
   <meta charset="UTF-8">
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   <meta http-equiv="X-UA-Compatible" content="ie=edge">
   <title>Site Layout</title>
</head>

<body>
   @yield('content')
</body>

</html>

```

## Controller home

```bash
 php artisan make:controller Site/HomeController
```



app\Http\Controllers\Site\HomeController.php

```php
<?php

namespace App\Http\Controllers\Site;

use App\Http\Controllers\Controller;
use Illuminate\Http\Request;

class HomeController extends Controller
{
    public function index()
    {
        return view("site.home");
    }
}
```

## View home

resources\views\site\home.blade.php

```php
@extends('layouts.site.site-layout')

@section('content')
   Home Page
@endsection

```

## Route

routes\web.php

```php
Route::get('/', [App\Http\Controllers\Site\HomeController::class, 'index'])->name('site.home');
```


