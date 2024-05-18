# C01E004P009 - Membuat Login Request



## Login Request

```bash
php artisan make:request Auth/LoginRequest
```

app\Http\Requests\Auth\LoginRequest.php

```php
<?php

namespace App\Http\Requests\Auth;

use Illuminate\Foundation\Http\FormRequest;
use Illuminate\Support\Facades\Auth;
use Illuminate\Validation\ValidationException;

class LoginRequest extends FormRequest
{
    public function authenticate()
    {
        $validated = $this->validated();
        $authenticate = Auth::attempt($validated);
        if (!$authenticate) {
            throw ValidationException::withMessages([
                'email' => trans('auth.failed'),
            ]);
        }
    }


    public function authorize(): bool
    {
        return true;
    }

    public function rules(): array
    {
        return [
            'email' => [
                'required',
                'string',
                'email'
            ],
            'password' => [
                'required',
                'string',
            ]
        ];
    }
}

```

## Controller Login

app\Http\Controllers\Auth\LoginController.php

```php
<?php

namespace App\Http\Controllers\Auth;

// another code...
use App\Http\Requests\Auth\LoginRequest;

class LoginController extends Controller
{
    // another code...
    public function action(LoginRequest $request)
    {
        $request->authenticate();

        $request->session()->regenerate();

        return redirect()->intended(route("dashboard.home", absolute: false));
    }
}


```

## Ref

- https://laravel.com/docs/11.x/requests

- https://medium.com/@kamerk22/the-smart-way-to-handle-request-validation-in-laravel-5e8886279271

- https://amanj0314.medium.com/laravel-validation-using-request-53f7f90ceff7


