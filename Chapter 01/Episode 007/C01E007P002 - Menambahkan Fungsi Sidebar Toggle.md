# C01E007P002 - Menambahkan Fungsi Sidebar Toggle

## Dashboard JS

resources\js\layouts\dashboard.js

```js
// Toggle the side navigation
function sidebarToggle() {
    const sidebarToggle = document.body.querySelector("#sidebarToggle");
    if (sidebarToggle) {
        sidebarToggle.addEventListener("click", (event) => {
            event.preventDefault();
            document.body.classList.toggle("sb-sidenav-toggled");
            localStorage.setItem(
                "sb|sidebar-toggle",
                document.body.classList.contains("sb-sidenav-toggled")
            );
        });
    }
}

window.addEventListener("DOMContentLoaded", () => {
    sidebarToggle();
});
```

resources\views\layouts\dashboard\dashboard-layout.blade.php

```php
@vite(['resources/js/app.js', 'resources/js/layouts/dashboard.js'])
```

## Config Vite

vite.config.js

```js
import { defineConfig } from "vite";
import laravel from "laravel-vite-plugin";

export default defineConfig({
    plugins: [
        laravel({
            input: [
                // another code
                "resources/js/layouts/dashboard.js",
            ],
            refresh: true,
        }),
    ],
});
```

## Ref

- [startbootstrap-sb-admin/src/js/scripts.js at master · StartBootstrap/startbootstrap-sb-admin · GitHub](https://github.com/StartBootstrap/startbootstrap-sb-admin/blob/master/src/js/scripts.js)
