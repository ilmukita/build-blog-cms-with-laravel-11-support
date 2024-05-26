# C01E012P003 - Pagination Data Tag

## TagController@index

app\Http\Controllers\Dashboard\TagController.php

```php
<?php
// method index
public function index()
{
    return view('dashboard.tag.index', [
        'tags' => Tag::paginate(10)
    ]);
}
```

## Render Pagination

resources\views\dashboard\tag\index.blade.php

```php
<div class="card-footer">
         {{ $tags->links() }}
</div>
```

## Using Bootstrap UI

```php
<?php
//namespace
use Illuminate\Pagination\Paginator;
// method index
public function boot()
{
    Paginator::useBootstrapFive();
}
```

## Ref

- [Database: Pagination - Laravel 11.x - The PHP Framework For Web Artisans](https://laravel.com/docs/11.x/pagination)


