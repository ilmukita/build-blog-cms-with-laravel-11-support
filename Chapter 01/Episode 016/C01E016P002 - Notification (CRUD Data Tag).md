# C01E016P002 - Notification (CRUD Data Tag)

## Create & Update

app\Http\Controllers\Dashboard\TagController.php

```php
<?php

namespace App\Http\Controllers\Dashboard;

use App\Http\Controllers\Controller;
use App\Http\Requests\Dashboard\Tag\UpSertTagRequest;
use App\Models\Tag;
use App\Support\Toaster;

class TagController extends Controller
{

    public function store(UpSertTagRequest $request)
    {
        Tag::create($request->validated());
        Toaster::make('Create Tag', "Tag data created successfully");
        return redirect(route('dashboard.tag'));
    }

    public function update(UpSertTagRequest $request, $slugId)
    {
        $tag = Tag::findOrFail($slugId);
        $tag->update($request->validated());
        Toaster::make('Update Tag', "Tag data updated successfully");
        return redirect(route('dashboard.tag'));
    }

    public function delete($slugId)
    {
        $tag = Tag::findOrFail($slugId);
        $tag->delete();
        Toaster::make('Delete Tag', "Tag data has been successfully deleted");
        return redirect()->back();
    }
}
```

## Validation

app\Http\Requests\Dashboard\Tag\UpSertTagRequest.php

```php
<?php

namespace App\Http\Requests\Dashboard\Tag;

use App\Support\Toaster;
use Illuminate\Foundation\Http\FormRequest;
use Illuminate\Contracts\Validation\Validator;

class UpSertTagRequest extends FormRequest
{
    protected function failedValidation(Validator $validator)
    {
        Toaster::error('Validation', summarizeValidation($validator));
    }

}
```

## Helper

app\Support\helpers.php

```php
if (!function_exists('summarizeValidation')) {

    /**
     * Create an error message summary from the validation errors.
     *
     * @param  \Illuminate\Contracts\Validation\Validator  $validator
     * @return string
     */
    function summarizeValidation($validator)
    {
        $messages = $validator->errors()->all();

        if (!count($messages) || !is_string($messages[0])) {
            return $validator->getTranslator()->get('The given data was invalid.');
        }

        $message = array_shift($messages);

        if ($count = count($messages)) {
            $pluralized = $count === 1 ? 'error' : 'errors';

            $message .= ' ' . $validator->getTranslator()->choice("(and :count more $pluralized)", $count, compact('count'));
        }

        return $message;
    }
}
```
