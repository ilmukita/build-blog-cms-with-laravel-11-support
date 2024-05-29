# C01E014P003 - Proses Update Tag

## Controller

app\Http\Controllers\Dashboard\TagController.php

```php
    public function update(Request $request, $slugId)
    {

        // validator

        $tag = Tag::findOrFail($slugId);
        $tag->update($validator->getData());
        return redirect(route('dashboard.tag'));
    }
```
