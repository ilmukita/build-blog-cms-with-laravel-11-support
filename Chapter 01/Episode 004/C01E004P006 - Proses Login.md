# C01E004P006 - Proses Login

app\Http\Controllers\Auth\LoginController.php

```php
// another code
use Illuminate\Support\Facades\Auth;
use Illuminate\Validation\ValidationException;

class LoginController extends Controller
{
    // another code

    public function action(Request $request)
    {

        // another code
        $authenticate = Auth::attempt([
         'email' => 'emailvalue',
         'password' => 'passwordvalue'
         ]);

        if ($authenticate) {
            $request->session()->regenerate();
            return redirect()->intended(route("dashboard.home", absolute: false));
        }

        throw ValidationException::withMessages([
            'email' => trans('auth.failed'),
        ]);
    }
}
```

## Ikhtisar

- `redirect()`: Fungsi ini digunakan untuk mengalihkan pengguna ke halaman lain.
- `intended()`: Bagian ini memberitahu Laravel untuk mencari tahu halaman yang coba diakses pengguna sebelumnya (intended URL).
- `route('dashboard.home', absolute: false)`: Bagian ini bertugas untuk membuat URL untuk route bernama `dashboard.home`. Parameter `absolute: false` adalah yang menjadi fokus kita kali ini.
- `absolute: false` digunakan untuk menghasilkan URL relatif, bukan URL absolut. Maksudnya, URL tidak akan menyertakan nama domain dan protokol lengkap (misalnya, `https://example.com`). Sebaliknya, hanya menyertakan path ke route tersebut (misalnya, `/dashboard/home`). Ini berguna ketika Anda ingin mengalihkan pengguna ke URL yang relatif terhadap halaman saat ini. 

## Ref

- [GitHub - laravel/breeze: Minimal Laravel authentication scaffolding with Blade, Vue, or React + Tailwind.](https://github.com/laravel/breeze)
