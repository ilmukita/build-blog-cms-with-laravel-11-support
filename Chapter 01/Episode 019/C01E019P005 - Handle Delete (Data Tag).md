# C01E019P005 - Handle Delete (Data Tag)

## Controller

app\Http\Controllers\Dashboard\TagController.php

```php
public function index(Request $request)
{
    //...
    return view('dashboard.tag.index', [
        //...
        'route' => [
            //...
            'edit' => route('dashboard.tag.delete', ['slugId' => ":tagId"]),
            //...
        ],
        //...
    ]);
}
```

## View

resources\views\dashboard\tag\index.blade.php

```php
         <table id="tableTag" class="table table-bordered table-hover nowrap" style="width:100%"
            data-ajax-url="{{ $route['list'] }}" data-route-create="{{ $route['create'] }}"
            data-route-edit="{{ $route['edit'] }}" data-route-delete="{{ $route['delete'] }}">
         </table>  
         
         
<form id="formDeleteTag" action="" method="POST">
         @csrf
         @method('DELETE')
      </form>         
```

## JS

resources\js\views\dashboard\tag\index.view.js

```js
function createDataTable() {
   //..
   const tableTag = new DataTable(tableTagEl, {
      //...
   });
   return tableTag;
}
```

```js
function handleDelete(dataTableEl) {
    const tableTagEl = document.getElementById("tableTag");
    const { routeDelete } = tableTagEl.dataset;
    const formDeleteTag = document.getElementById("formDeleteTag");

    dataTableEl.on(
        "click",
        `button[data-action-name='buttonDelete']`,
        function (e) {
            const data = dataTableEl.row(e.target.closest("tr")).data();
            const action = routeDelete.replace(":tagId", data.id);
            formDeleteTag.action = action;
            formDeleteTag.submit();
        }
    );
}
```

```js
window.addEventListener("DOMContentLoaded", () => {
    const tableTag = createDataTable();
    handleDelete(tableTag);
});
```


