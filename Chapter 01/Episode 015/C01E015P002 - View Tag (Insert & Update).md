# C01E015P002 - View Tag (Insert & Update)

## View Insert & Update

resources\views\dashboard\tag\_upsert.blade.php

```php
<div class="card">
   <div class="card-body">
      <form id="formTag" action="{{ $form['route'] }}" method="POST">
         @method($form['method'])
         @csrf
         <label for="inputTitle" class="form-label">Title</label>
         <input name="title" type="text" id="inputTitle" value="{{ old('title', $input['title']) }}"
            @class(['form-control', 'is-invalid' => isInvalidError('title')])>
         <div id="textSlug" class="form-text">
            {{ old('slug', $input['slug']) }}
         </div>
         <input name="slug" type="hidden" id="inputSlug" value="{{ old('slug', $input['slug']) }}">
         <x-error.invalid-feedback fieldName="title" />
      </form>
   </div>
   <div class="card-footer bg-white border-top-0">
      <div class="d-flex flex-row-reverse">
         <div class="gap-3">
            <button data-route="{{ $route['back'] }}" id="buttonBack" type="button" class="btn btn-secondary">
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

resources\views\dashboard\tag\create.blade.php

```php
@extends('layouts.dashboard.dashboard-layout')

@section('title', 'Create Tag')

@section('breadcrumb')
   {{ Breadcrumbs::render('db-tags-create') }}
@endsection

@section('content')
   @include('dashboard.tag._upsert', [
       'input' => [
           'title' => null,
           'slug' => null,
       ],
   ])
@endsection

@push('script-internal')
   @vite('resources/js/views/dashboard/tag/upsert.view.js')
@endpush
```

resources\views\dashboard\tag\edit.blade.php

```php
@extends('layouts.dashboard.dashboard-layout')

@section('title', 'Edit Tag')

@section('breadcrumb')
   {{ Breadcrumbs::render('db-tags-edit', $tag) }}
@endsection

@section('content')
   @include('dashboard.tag._upsert', [
       'input' => [
           'title' => $tag->title,
           'slug' => $tag->slug,
       ],
   ])
@endsection

@push('script-internal')
   @vite('resources/js/views/dashboard/tag/upsert.view.js')
@endpush
```

Config Vite

vite.config.js

```js
export default defineConfig({
    plugins: [
        laravel({
            input: [
                // remove - :"resources/js/views/dashboard/tag/create.view.js",
                // remove - :"resources/js/views/dashboard/tag/edit.view.js",
                "resources/js/views/dashboard/tag/upsert.view.js",
            ],
            refresh: true,
        }),
    ],
});
```


