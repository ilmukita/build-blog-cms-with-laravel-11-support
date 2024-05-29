# C01E015P001 - Request Tag (Insert & Update)

## Create Request

```bash
 php artisan make:request Dashboard/Tag/UpSertTagRequest
```

app\Http\Requests\Dashboard\Tag\UpSertTagRequest.php

```php
<?php

namespace App\Http\Requests\Dashboard\Tag;

use Illuminate\Foundation\Http\FormRequest;
use Illuminate\Support\Facades\Validator as FValidator;
use Illuminate\Contracts\Validation\Validator;

class UpSertTagRequest extends FormRequest
{
    private Validator $validatorSlug;

    public function authorize(): bool
    {
        return true;
    }

    public function validated($key = null, $default = null)
    {
        return data_get(
            array_merge(
                $this->validator->validated(),
                $this->validatorSlug->validated()
            ),
            $key,
            $default
        );
    }

    public function withValidator(Validator $validator)
    {

        $validator->after(function ($validator) {
            $validator->setValue('slug', 'aa');
            $slugValidator = $this->makeSlugValidator();
            if ($slugValidator->fails()) {
                $validator->errors()->add('title', $slugValidator->errors()->get("slug"));
            }
        });
    }

    public function rules(): array
    {
        return [
            'title' => ['required', 'string', 'min:3', 'max:60'],
        ];
    }

    protected function makeSlugValidator()
    {
        $slugId = $this->route('slugId');
        $uniqueRule = $this->method() == 'PUT' ? 'unique:tags,slug,' . $slugId : 'unique:tags,slug';
        $this->validatorSlug = FValidator::make(
            $this->only('slug'),
            [
                'slug' => ['required', 'string', $uniqueRule],
            ],
            attributes: [
                'slug' => 'title'
            ]
        );

        return $this->validatorSlug;
    }
}
```

app\Http\Controllers\Dashboard\TagController.php

```php
use App\Http\Requests\Dashboard\Tag\UpSertTagRequest;
```

```php
    public function store(UpSertTagRequest $request)
    {
        //code...
    }

    public function update(UpSertTagRequest $request, $slugId)
    {
        // code...
    }
```
