# C01E018P004 - Search Data Tag (AJAX)

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
        $search = $request->input('search.value');

        if ($search) {
            $query->where('title', 'LIKE', '%' . $search . '%');
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
}
```
