# C01E018P005 - Sorting Data Tag (AJAX)

## Controller (TagController@list)

app\Http\Controllers\Dashboard\TagController.php

```php
    public function list(Request $request)
    {
        $query = Tag::query();
        $recordsTotal = Tag::count();

        $draw = $request->query('draw', 1);
        $offset = $request->query('start', 0);
        $perPage = $request->query('length', 10);
        $search = $request->input('search.value');
        $orderColumn = $request->input('order.0.name');
        $orderDirection = $request->input('order.0.dir');

        if ($search) {
            $query->where('title', 'LIKE', '%' . $search . '%');
        }

        if ($orderColumn && $orderDirection) {
            $query->orderBy($orderColumn, $orderDirection);
        } else {
            $query->orderBy('created_at', 'desc');
        }

        $recordsFiltered = $query->count();
        $tags = $query->limit($perPage)->offset($offset)->get();
        return response()->json([
            'draw' => $draw,
            'recordsTotal' => $recordsTotal,
            'recordsFiltered' => $recordsFiltered,
            'data' => $tags
        ]);
    }
```

## JS

resources\js\views\dashboard\tag\index.view.js

```js
function createDataTable() {
    const tableTag = new DataTable(tableTagEl, {
        order: [],
        // ...
    });
}
```
