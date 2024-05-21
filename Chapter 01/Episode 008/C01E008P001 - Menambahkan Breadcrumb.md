# C01E008P001 - Menambahkan Breadcrumb

config\breadcrumbs.php

```php
'files' => base_path('breadcrumbs/web.php'),
```

breadcrumbs\web.php

```php
<?php

use Diglactic\Breadcrumbs\Breadcrumbs;
use Diglactic\Breadcrumbs\Generator as BreadcrumbTrail;

// Dashboard
Breadcrumbs::for('dashboard', function (BreadcrumbTrail $trail) {
    $trail->push('Dashboard', route('dashboard.home'));
});
```

resources\views\layouts\\**\ *-layout.blade.php

```php
{{-- @include('layouts.dashboard._breadcrumb') --}}
@yield('breadcrumb')
```

resources\views\\**\\*.blade.php

```php
@section('breadcrumb')
   {{ Breadcrumbs::render('dashboard') }}
@endsection
```

# Ref

- [GitHub - diglactic/laravel-breadcrumbs: Laravel Breadcrumbs - A simple Laravel-style way to create breadcrumbs.](https://github.com/diglactic/laravel-breadcrumbs)

- [diglactic/laravel-breadcrumbs - Packagist](https://packagist.org/packages/diglactic/laravel-breadcrumbs)
