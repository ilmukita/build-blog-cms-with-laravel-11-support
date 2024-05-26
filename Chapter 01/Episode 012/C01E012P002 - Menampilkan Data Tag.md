# C01E012P002 - Menampilkan Data Tag

## TagController@index

app\Http\Controllers\Dashboard\TagController.php

```php
<?php
// namespace
use App\Models\Tag;
// method index
public function index()
{
    return view('dashboard.tag.index', [
        'tags' => Tag::take(10)->get()
    ]);
}
```

## Tag List

resources\views\dashboard\tag\index.blade.php

```php
   <div class="card">
      <div class="card-body">
         <table class="table table-bordered table-hover">
            <thead>
               <tr>
                  <th>Tag</th>
                  <th>Action</th>
               </tr>
            </thead>
            <tbody>
               @foreach ($tags as $tag)
                  <tr>
                     <td>{{ $tag->title }}</td>
                     <td>
                        <button type="button" class="btn btn-primary">Edit</button>
                        <button type="button" class="btn btn-danger">Delete</button>
                     </td>
                  </tr>
               @endforeach
            </tbody>
         </table>
      </div>
   </div>
```
