# C01E013P002 - Membuat Halaman Tambah Tag (JS)

## Create File Javascript

resources\js\views\dashboard\tag\create.view.js

```js
function handleBack() {
    const buttonBack = document.getElementById("buttonBack");
    const route = buttonBack.getAttribute("data-route");
    buttonBack.addEventListener("click", () => {
        window.location = route;
    });
}

window.addEventListener("DOMContentLoaded", () => {
    handleBack();
});
```

resources\views\dashboard\tag\create.blade.php

```php
@push('script-internal')
   @vite('resources/js/views/dashboard/tag/create.view.js')
@endpush
```

resources\views\layouts\dashboard\dashboard-layout.blade.php

```php
@stack('script-internal')
```

## Config Vite

vite.config.js

```js
export default defineConfig({
    plugins: [
        laravel({
            input: [
                // another code...
                "resources/js/views/dashboard/tag/create.view.js",
            ],
            refresh: true,
        }),
    ],
});
```

## Ref

- [Blade Templates - Laravel 11.x - The PHP Framework For Web Artisans](https://laravel.com/docs/11.x/blade#stacks)

- [The Power of @stack in Laravel's Blade - DEV Community](https://dev.to/faridteymouri/the-power-of-stack-in-laravels-blade-4g3b)
