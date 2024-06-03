# C01E019P002 - Add Button Create Tag

## View

resources\views\dashboard\tag\index.blade.php

```php
<table id="tableTag" class="table table-bordered table-hover nowrap" style="width:100%"
            data-ajax-url="{{ $route['list'] }}" data-route-create="{{ $route['create'] }}">
```

## JS

resources\js\views\dashboard\tag\index.view.js

```js
function createDataTable() {
    const tableTagEl = document.getElementById("tableTag");
    const { ajaxUrl, routeCreate } = tableTagEl.dataset;
    const tableTag = new DataTable(tableTagEl, {
        layout: {
            top2Start: {
                buttons: [
                    {
                        text: "Create",
                        className: "btn btn-primary",
                        action: () => {
                            window.location = routeCreate;
                        },
                    },
                ],
            },
        },
        //...
    });
}
```

## Plugin

resources\js\plugins\dataTable.js

```js
import DataTable from "datatables.net-bs5";
import "datatables.net-buttons-bs5";

DataTable.Buttons.defaults.dom.button.className = "btn";

export { DataTable };
```

## Ref

- [layout](https://datatables.net/reference/option/layout)

- [classname not working on buttons](https://datatables.net/forums/discussion/78459/classname-not-working-on-buttons)
