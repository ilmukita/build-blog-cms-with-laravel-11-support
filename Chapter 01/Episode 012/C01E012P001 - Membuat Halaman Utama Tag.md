# C01E012P001 - Membuat Halaman Utama Tag

## Create view

```bash
php artisan make:view dashboard/tag/index
```

resources\views\dashboard\tag\index.blade.php

```php
@extends('layouts.dashboard.dashboard-layout')

@section('title', 'Tags')

@section('breadcrumb')
   {{ Breadcrumbs::render('db-tags') }}
@endsection

@section('content')
   Tag list
@endsection
```

## Create Controller

```bash
php artisan make:controller Dashboard/TagController
```

app\Http\Controllers\Dashboard\TagController.php

```php
<?php

namespace App\Http\Controllers\Dashboard;

use App\Http\Controllers\Controller;
use Illuminate\Http\Request;

class TagController extends Controller
{
    public function index()
    {
        return view('dashboard.tag.index');
    }
}
```

## Add Breadcrumb

breadcrumbs\web.php

```php
// Dashboard > Tags
Breadcrumbs::for('db-tags', function (BreadcrumbTrail $trail) {
    $trail->parent('dashboard');
    $trail->push('Tags', route('dashboard.tag'));
});
```

## Add Sidenav Menu

app\View\Composers\DashboardComposer.php

```php
[
    'heading' => "Blog",
    'menus' => [
        [
            'title' => 'Tags',
            'icon' => 'bi-tags',
            'route' => route('dashboard.tag'),
        ]
    ]
]
```

## Route

routes\web.php

```php
Route::get('/dashboard/tags', [TagController::class, 'index'])->name('dashboard.tag');
```
