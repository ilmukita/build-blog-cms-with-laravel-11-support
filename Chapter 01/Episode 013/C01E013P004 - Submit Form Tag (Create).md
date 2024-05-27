# C01E013P004 - Submit Form Tag (Create)

## Route store tag

routes\web.php

```php
Route::post('/dashboard/tags/create', [TagController::class, 'store'])->name('dashboard.tag.store');
```

## Tag Controller

app\Http\Controllers\Dashboard\TagController.php

```php
    public function create()
    {
        return view('dashboard.tag.create', [
            'form' => [
                'route' => route('dashboard.tag.store'),
                'method' => 'POST',
            ],
        ]);
    }

    public function store(Request $request)
    {
        dd($request->all());
    }
```

## Form Tag

resources\views\dashboard\tag\create.blade.php

```php
         <form id="formTag" action="{{ $form['route'] }}" method="POST">
            @csrf
            <label for="inputTitle" class="form-label">Title</label>
            <input name="title" type="text" id="inputTitle" class="form-control">
            <div id="textSlug" class="form-text">
               slug-title
            </div>
            <input name="slug" type="hidden" id="inputSlug">
         </form>
```

## Handle Submit

resources\js\views\dashboard\tag\create.view.js

```javascript
function handleSubmit() {
    const formTag = document.getElementById("formTag");
    const buttonSave = document.getElementById("buttonSave");
    buttonSave.addEventListener("click", () => {
        formTag.submit();
    });
}

window.addEventListener("DOMContentLoaded", () => {    
    handleSubmit();
});
```
