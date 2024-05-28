# C01E014P002 - Validasi Form Tag (Update)

## Controller

app\Http\Controllers\Dashboard\TagController.php

```php
    public function update(Request $request, $slugId)
    {

        $validator = Validator::make($request->all(), [
            'title' => ['required', 'string', 'min:3', 'max:60'],
        ]);

        $validator->after(function ($validator) use ($request, $slugId) {
            if ($validator->errors()->isEmpty()) {
                $slugValidator = Validator::make(
                    $request->all(),
                    [
                        'slug' => [
                            'required',
                            'string',
                            'unique:tags,slug,' . $slugId
                        ],
                    ],
                    attributes: [
                        'slug' => 'title'
                    ]
                );

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
    }
```
