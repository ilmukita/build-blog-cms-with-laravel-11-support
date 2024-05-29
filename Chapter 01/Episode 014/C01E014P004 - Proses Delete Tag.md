# C01E014P004 - Proses Delete Tag

## Route

routes\web.php

```php
Route::delete('/dashboard/tags/{slugId}', [TagController::class, 'delete'])->name('dashboard.tag.delete');
```

## Controller

app\Http\Controllers\Dashboard\TagController.php

```php
    public function delete($slugId)
    {
        $tag = Tag::findOrFail($slugId);
        $tag->delete();
        return redirect()->back();
    }
```

## View

resources\views\dashboard\tag\index.blade.php

```php
<button id="buttonEdit" data-route="{{ route('dashboard.tag.edit', ['slugId' => $tag->id]) }}"
                           type="button" class="btn btn-primary">Edit</button>


<form id="formDeleteTag" action="" method="POST">
         @csrf
         @method('DELETE')
      </form>
```

## JS

resources\js\views\dashboard\tag\index.view.js

```js
function handleDelete() {
    const buttonDelete = document.querySelectorAll("button#buttonDelete");
    const formDeleteTag = document.getElementById("formDeleteTag");
    buttonDelete.forEach((btnDelete) => {
        const route = btnDelete.getAttribute("data-route");
        btnDelete.addEventListener("click", () => {
            formDeleteTag.action = route;
            formDeleteTag.submit();
        });
    });
} 
```

```js
window.addEventListener("DOMContentLoaded", () => {
    // another code
    handleDelete();
});
```
