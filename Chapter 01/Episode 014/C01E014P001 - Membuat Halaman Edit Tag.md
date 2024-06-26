# C01E014P001 - Membuat Halaman Edit Tag

## Route

routes\web.php

```php
    Route::get('/dashboard/tags/{slugId}/edit', [TagController::class, 'edit'])->name('dashboard.tag.edit');
    Route::put('/dashboard/tags/{slugId}', [TagController::class, 'update'])->name('dashboard.tag.update');
```

## Breadcrums

breadcrumbs\web.php

```php
// Dashboard > Tags > Edit > [title]
Breadcrumbs::for('db-tags-edit', function (BreadcrumbTrail $trail, $tag) {
    $route = route('dashboard.tag.edit', [
        'slugId' => $tag->id
    ]);
    $trail->parent('db-tags');
    $trail->push('Edit', $route);
    $trail->push($tag->title, $route);
});
```

## Controller

app\Http\Controllers\Dashboard\TagController.php

```php
    public function edit($slugId)
    {
        $tag = Tag::findOrFail($slugId);
        return view('dashboard.tag.edit', [
            'tag' => $tag,
            'form' => [
                'route' => route('dashboard.tag.update', ['slugId' => $slugId]),
                'method' => 'PUT',
            ],
            'route' => [
                'back' => route('dashboard.tag')
            ]
        ]);
    }

    public function update(Request $request, $slugId)
    {
        dd($request->all(), $slugId);        
    }
```

## View

resources\views\dashboard\tag\index.blade.php

```php
<button id="buttonEdit" data-route="{{ route('dashboard.tag.edit', ['slugId' => $tag->id]) }}"
                           type="button" class="btn btn-primary">Edit</button>
```

## JS

resources\js\views\dashboard\tag\index.view.js

```js
function handleEdit() {
    const buttonEdit = document.querySelectorAll("button#buttonEdit");
    buttonEdit.forEach((btnEdit) => {
        const route = btnEdit.getAttribute("data-route");
        btnEdit.addEventListener("click", () => {
            window.location = route;
        });
    });
} 
```

```js
window.addEventListener("DOMContentLoaded", () => {
    handleEdit();
});
```

## Config Vite

vite.config.js

```js
export default defineConfig({
    plugins: [
        laravel({
            input: [
                // another code...
                "resources/js/views/dashboard/tag/index.view.js",
                "resources/js/views/dashboard/tag/edit.view.js",
            ],
            refresh: true,
        }),
    ],
});
```
