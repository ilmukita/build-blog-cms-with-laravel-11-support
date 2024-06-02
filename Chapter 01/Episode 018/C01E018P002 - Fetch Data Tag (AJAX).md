# C01E018P002 - Fetch Data Tag (AJAX)

## Route

routes\web.php

```php
Route::get('/dashboard/tags/list', [TagController::class, 'list'])->name('dashboard.tag.list');
```

## Controller (TagController@list)

app\Http\Controllers\Dashboard\TagController.php

```php
<?php

namespace App\Http\Controllers\Dashboard;

use App\Http\Controllers\Controller;
use App\Models\Tag;

class TagController extends Controller
{
    public function list()
    {
        $tags = Tag::all();
        return response()->json([
            'draw' => 1,
            'recordsTotal' => $tags->count(),
            'recordsFiltered' => $tags->count(),
            'data' => $tags
        ]);
    }
}
```

## JS

resources\js\views\dashboard\tag\index.view.js

```js
function createDataTable() {
    const tableTagEl = document.getElementById("tableTag");
    const { ajaxUrl } = tableTagEl.dataset;
    const tableTag = new DataTable(tableTagEl, {
        ajax: {
            url: ajaxUrl,
        },
        columns: [{ title: "Tag", data: "title" }],
    });
}
```

## Ref

- [Server-side processing](https://datatables.net/manual/server-side)
