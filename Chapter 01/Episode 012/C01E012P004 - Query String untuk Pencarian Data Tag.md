# C01E012P004 - Query String untuk Pencarian Data Tag



## Template Form Search

```html
<div class="d-flex">
   <div class="flex-grow-1">
      <!-- Action create -->
   </div>
   <div>
      <form class="d-flex" role="search" action="" method="GET">
         <input name="q" value="" class="form-control me-2" type="search"
            placeholder="Search..." aria-label="Search">
         <button class="btn btn-primary" type="submit">
            Search
         </button>
      </form>
   </div>
</div>
```

## TagController@index

app\Http\Controllers\Dashboard\TagController.php

```php

<?php

namespace App\Http\Controllers\Dashboard;

use App\Http\Controllers\Controller;
use App\Models\Tag;
use Illuminate\Http\Request;
use Illuminate\Support\Str;

class TagController extends Controller
{
    public function index(Request $request)
    {
        $q = Str::trim($request->query('q'));
        $tags = [];

        if ($q) {
            $tags = Tag::where('title', 'LIKE', "%{$q}%")->paginate(10)->withQueryString();
        } else {
            $tags = Tag::paginate(10);
        }

        return view('dashboard.tag.index', [
            'tags' => $tags,
            'route' => [
                'search' => route('dashboard.tag')
            ],
            'queryString' => [
                'q' => $q
            ]
        ]);
    }
}

```

## Form Search

resources\views\dashboard\tag\index.blade.php

```php
<div class="d-flex">
   <div class="flex-grow-1"></div>
   <div>
      <form class="d-flex" role="search" action="{{ $route['search'] }}" method="GET">
         <input name="q" value="{{ $queryString['q'] }}" class="form-control me-2" type="search"
            placeholder="Search..." aria-label="Search">
         <button class="btn btn-primary" type="submit">
            <x-icon.bs-icon name="bi-search" />
         </button>
      </form>
   </div>
</div>
```
