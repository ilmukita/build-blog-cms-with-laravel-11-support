# C01E013P005 - Validasi Form Tag (Create)

## Controller

app\Http\Controllers\Dashboard\TagController.php

```php
use Illuminate\Support\Facades\Validator;
use Illuminate\Validation\ValidationException;
```

```php
    public function store(Request $request)
    {
        $validator = Validator::make($request->all(), [
            'title' => ['required', 'string', 'min:3', 'max:60'],
        ]);

        $validator->after(function ($validator) use ($request) {
            if ($validator->errors()->isEmpty()) {
                $slugValidator = Validator::make($request->all(), [
                    'slug' => ['required', 'string', 'unique:tags,slug'],
                ],
                 attributes: [
                    'slug' => 'title'
                ]);

                if ($slugValidator->fails()) {
                    foreach ($slugValidator->errors()->all() as $error) {
                        $validator->errors()->add('title', $error);
                    }
                }
            }
        });

        if ($validator->fails()) {
            throw ValidationException::withMessages($validator->errors()->messages());
        }
        dd($validator->getData());
    }
```

## View

resources\views\dashboard\tag\create.blade.php

```php
@section('content')
   <div class="card">
      <div class="card-body">
         <form id="formTag" action="{{ $form['route'] }}" method="POST">
            @csrf
            <label for="inputTitle" class="form-label">Title</label>
            <input name="title" type="text" id="inputTitle" value="{{ old('title') }}" @class(['form-control', 'is-invalid' => isInvalidError('title')])>
            <div id="textSlug" class="form-text">
               {{ old('slug') }}
            </div>
            <input name="slug" type="hidden" id="inputSlug" value="{{ old('slug') }}">
            <x-error.invalid-feedback fieldName="title" />
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

## Ref

- [Laravel Validation - Laravel News](https://laravel-news.com/validation)

- https://laravel.com/docs/11.x/validation
