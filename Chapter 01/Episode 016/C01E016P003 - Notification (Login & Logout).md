# C01E016P003 - Notification (Login & Logout)



## JS

resources\js\layouts\auth.js

```js
import { loadToaster } from "../plugins/toaster";

window.addEventListener("DOMContentLoaded", () => {
    loadToaster();
});

```

## Layout

resources\views\layouts\auth\auth-layout.blade.php

```php
{{-- another code --}}
<body class="bg-primary">
   @include('toaster.toasts')
   {{-- another code --}}
   @vite(['resources/js/app.js', 'resources/js/layouts/auth.js'])
</body>
{{-- another code --}}
```

## Vite

vite.config.js

```js
export default defineConfig({
    plugins: [
        laravel({
            input: [                
                // another code ...
                "resources/js/layouts/auth.js",
                // another code ...
            ],
            refresh: true,
        }),
    ],
});
```



## Login

app\Http\Controllers\Auth\LoginController.php

```php
<?php

namespace App\Http\Controllers\Auth;

use App\Http\Controllers\Controller;
use App\Http\Requests\Auth\LoginRequest;
use App\Support\Toaster;

class LoginController extends Controller
{
    public function action(LoginRequest $request)
    {
        $request->authenticate();

        $request->session()->regenerate();
        Toaster::success('Login', 'Login successful');
        return redirect()->intended(route("dashboard.home", absolute: false));
    }
}

```

app\Http\Requests\Auth\LoginRequest.php

```php
<?php

namespace App\Http\Requests\Auth;

use App\Support\Toaster;
use Illuminate\Contracts\Validation\Validator;
use Illuminate\Foundation\Http\FormRequest;

class LoginRequest extends FormRequest
{

    protected function failedValidation(Validator $validator)
    {
        Toaster::error('Validation', summarizeValidation($validator));
    }
}

```

## Logout

app\Http\Controllers\Auth\LogoutController.php

```php
<?php

namespace App\Http\Controllers\Auth;

use App\Http\Controllers\Controller;
use App\Support\Toaster;
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
        Toaster::success('Logout', 'Logout successful');
        return redirect()->intended(route('auth.login'));
    }
}

```


