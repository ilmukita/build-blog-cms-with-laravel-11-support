# C01E005P001 - Menambahkan Action Logout

## Controller logout

```bash
php artisan make:controller Auth/LogoutController -i
```

routes\web.php

```php
use App\Http\Controllers\Auth\{LoginController, LogoutController};
// use App\Http\Controllers\Auth\LogoutController;

Route::middleware('auth')->group(function () {
    Route::post('/logout', LogoutController::class)->name('auth.logout');
});
```

app\Http\Controllers\Auth\LogoutController.php

```php
<?php

namespace App\Http\Controllers\Auth;

use App\Http\Controllers\Controller;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Auth;

class LogoutController extends Controller
{
    /**
     * Handle the incoming request.
     */
    public function __invoke(Request $request)
    {
        Auth::logout();

        $request->session()->invalidate();

        $request->session()->regenerateToken();

        return redirect()->intended(route('auth.login'));
    }
}
```

## Form Logout

resources\views\dashboard\home\index.blade.php

```php
@extends('layouts.dashboard.dashboard-layout')

@section('content')
   Dashboard Page
   <form action="{{ @route('auth.logout') }}" method="POST">
      @csrf
      <button type="submit">Logout</button>
   </form>
@endsection

```



## Ref

- https://laravel.com/docs/11.x/controllers#single-action-controllers

- [Laravel Invokable Controller - DEV Community](https://dev.to/ahmetkorkmaz3/laravel-invokable-controller-2gbj)

- https://www.php.net/manual/en/language.namespaces.importing.php


