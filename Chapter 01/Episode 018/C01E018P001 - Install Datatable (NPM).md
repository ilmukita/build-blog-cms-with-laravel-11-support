# C01E018P001 - Install Datatable (NPM)

## Install Datatable (Bootstrap 5)

```bash
 npm install datatables.net-bs5@^2.0.8 --save-dev
```

## Style (SCSS)

resources\sass\vendors\_datatable.scss

```sass
@import "datatables.net-bs5/css/dataTables.bootstrap5.css"
```

resources\sass\app.scss

```sass
// vendors
@import "./vendors/datatable";
```

## Plugin

resources\js\plugins\datatable.js

```js
import DataTable from "datatables.net-bs5";

export { DataTable };
```

## Use

### View

resources\views\dashboard\tag\index.blade.php

```php
<table id="tableTag" class="table table-bordered table-hover"></table>
```

### JS

resources\js\views\dashboard\tag\index.view.js

```js
import { DataTable } from "@/plugins/datatable";
```

```js
function createDataTable() {
    const tableTagEl = document.getElementById("tableTag");
    const tableTag = new DataTable(tableTagEl, {
        data: [],
        columns: [{ title: "Tag", data: "title" }],
    });
}
```

```js
window.addEventListener("DOMContentLoaded", () => {
    createDataTable();
});
```

## Ref

- [Datatable Download](https://datatables.net/download/)
