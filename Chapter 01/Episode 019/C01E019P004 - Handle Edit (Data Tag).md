# C01E019P004 - Handle Edit (Data Tag)

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
            'edit' => route('dashboard.tag.edit', ['slugId' => ":tagId"]),
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
            data-route-edit="{{ $route['edit'] }}">
         </table>
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
function handleEdit(dataTableEl) {
    const tableTagEl = document.getElementById("tableTag");
    const { routeEdit } = tableTagEl.dataset;

    dataTableEl.on(
        "click",
        `button[data-action-name='buttonEdit']`,
        function (e) {
            const data = dataTableEl.row(e.target.closest("tr")).data();
            const url = routeEdit.replace(":tagId", data.id);
            window.location.href = url;
        }
    );
}
```

```js
window.addEventListener("DOMContentLoaded", () => {
    const tableTag = createDataTable();
    handleEdit(tableTag);
});
```
