# C01E004P008 - Perbaiki Route [login] not defined

## Cara 1: buat route dengan nama "login"

routes\web.php

```php
Route::middleware('guest')->group(function () {
    Route::post('/path-login',/* array|callable|string|null */)->name('login');
});
```

## Cara 2: custom redirectGuestsTo

bootstrap\app.php

```php
use Illuminate\Http\Request;

->withMiddleware(function (Middleware $middleware) {
    $middleware->redirectGuestsTo(fn (Request $request) => route('routename'));
})
```

## Ref

- https://laravel.com/docs/11.x/authentication#redirecting-unauthenticated-users
