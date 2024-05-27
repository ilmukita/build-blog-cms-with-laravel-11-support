# C01E013P001 - Membuat Halaman Tambah Tag

## Template Page

```php
<div class="card">
   <div class="card-body">
      <form id="formTag" action="" method="POST">
         <label for="inputTitle" class="form-label">Title</label>
         <input name="title" type="text" id="inputTitle" class="form-control">
         <div id="textSlug" class="form-text">
            slug-title
         </div>
         <input name="slug" type="hidden" id="inputSlug">
      </form>
   </div>
   <div class="card-footer bg-white border-top-0">
      <div class="d-flex flex-row-reverse">
         <div class="gap-3">
            <button id="buttonBack" type="button" class="btn btn-secondary">
               Back
            </button>
            <button id="buttonSave" type="button" class="btn btn-primary">
               Save
            </button>
         </div>
      </div>
   </div>
</div>
```

## Route create

routes\web.php

```php
Route::get('/dashboard/tags/create', [TagController::class, 'create'])->name('dashboard.tag.create');
```

## Breadcrumb

breadcrumbs\web.php

```php
Breadcrumbs::for('db-tags-create', function (BreadcrumbTrail $trail) {
    $trail->parent('db-tags');
    $trail->push('Create', route('dashboard.tag.create'));
});
```

## Controller

app\Http\Controllers\Dashboard\TagController.php

```php
    public function index(Request $request)
    {
        //
        return view('dashboard.tag.index', [
            //
            'route' => [
                //
                'create' => route('dashboard.tag.create')
            ],
            //
        ]);
    }

    public function create()
    {
        return view('dashboard.tag.create', [
            'form' => [
                'route' => '/',
            ],
        ]);
    }
```

## View

resources\views\dashboard\tag\create.blade.php

```php
@extends('layouts.dashboard.dashboard-layout')

@section('title', 'Create Tag')

@section('breadcrumb')
   {{ Breadcrumbs::render('db-tags-create') }}
@endsection

@section('content')
   <div class="card">
      <div class="card-body">
         <form id="formTag" action="" method="POST">
            <label for="inputTitle" class="form-label">Title</label>
            <input name="title" type="text" id="inputTitle" class="form-control">
            <div id="textSlug" class="form-text">
               slug-title
            </div>
            <input name="slug" type="hidden" id="inputSlug">
         </form>
      </div>
      <div class="card-footer bg-white border-top-0">
         <div class="d-flex flex-row-reverse">
            <div class="gap-3">
               <button id="buttonBack" type="button" class="btn btn-secondary">
                  Back
               </button>
               <button id="buttonSave" type="button" class="btn btn-primary">
                  Save
               </button>
            </div>
         </div>
      </div>
   </div>
@endsection
```
