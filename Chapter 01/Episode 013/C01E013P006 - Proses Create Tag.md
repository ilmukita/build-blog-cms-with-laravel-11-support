# C01E013P006 - Proses Create Tag

app\Http\Controllers\Dashboard\TagController.php

```php
    public function store(Request $request)
    {
        //nother code...
        Tag::create($validator->getData());
        return redirect(route('dashboard.tag'));
    }
```


