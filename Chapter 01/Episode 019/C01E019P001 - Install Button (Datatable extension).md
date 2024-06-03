# C01E019P001 - Install Button (Datatable extension)

## Install Button (NPM)

```bash
npm install datatables.net-buttons-bs5@^3.0.2 --save-dev
```

resources\js\plugins\datatable.js

```js
import DataTable from "datatables.net-bs5";
import "datatables.net-buttons-bs5";
```

## Use

resources\js\views\dashboard\tag\index.view.js

```js
function createDataTable() {
    const tableTag = new DataTable(tableTagEl, {
        layout: {
            top: {
                buttons: [
                    {
                        text: "Create",
                    },
                ],
            },
        },
        // ...
    });
}
```
