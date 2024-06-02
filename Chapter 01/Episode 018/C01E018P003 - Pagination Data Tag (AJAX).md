# C01E018P003 - Pagination Data Tag (AJAX)

## Controller (TagController@list)

app\Http\Controllers\Dashboard\TagController.php

```php
<?php

namespace App\Http\Controllers\Dashboard;

use App\Http\Controllers\Controller;
use App\Models\Tag;
use Illuminate\Http\Request;

class TagController extends Controller
{
    public function list(Request $request)
    {
        $query = Tag::query();
        $recordsTotal = Tag::count();

        $draw = $request->query('draw', 1);
        $offset = $request->query('start', 0);
        $perPage = $request->query('length', 10);
        $recordsFiltered = $query->count();
        $tags = $query->limit($perPage)->offset($offset)->get();
        return response()->json([
            'draw' => $draw,
            'recordsTotal' => $recordsTotal,
            'recordsFiltered' => $recordsFiltered,
            'data' => $tags
        ]);
    }
}
```

## JS

resources\js\views\dashboard\tag\index.view.js

```js
function createDataTable() {
    const tableTag = new DataTable(tableTagEl, {
        serverSide: true,
        // ...
    });
}
```

## Ref

- https://www.webhadecreative.com/blog/2023/02/18/how-to-implement-datatables-server-side-processing-with-ajax-pagination-in-laravel/
