# C01E017P001 - Config Javascript (Alias Path)

## Config  Alias Path

jsconfig.json

```javascript
{
    "compilerOptions": {
        "baseUrl": ".",
        "paths": {
            "@/*": ["resources/js/*"],
        }
    },
    "exclude": ["node_modules", "public"]
}

```

```js
//resources\js\app.js
import { bootstrap, enableTooltip, enablePopover } from "@/plugins/bootstrap";
// resources\js\layouts\auth.js
import { loadToaster } from "@/plugins/toaster";
// resources\js\layouts\dashboard.js
import { loadToaster } from "@/plugins/toaster";
// resources\js\views\dashboard\tag\upsert.view.js
import { generateSlug } from "@/plugins/slugify";
```


