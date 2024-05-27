# C01E013P001 - Membuat Halaman Tambah Tag

## Template Page

```php
<div class="card">
   <div class="card-body">
      <form id="formTag" action="" method="POST">
         <label for="inputTitle" class="form-label">Title</label>
         <input type="password" id="inputTitle" class="form-control">
         <div id="textSlug" class="form-text">
            slug-title
         </div>
      </form>
   </div>
   <div class="card-footer bg-white border-top-0">
      <div class="d-flex flex-row-reverse">
         <div class="gap-3">
            <button id="buttonBack" type="button" class="btn btn-secondary">
               Back
            </button>
            <button id="buttonSave" type="button" class="btn btn-primary">
               Save
            </button>
         </div>
      </div>
   </div>
</div>
```

## Ref

- [Blade Templates - Laravel 11.x - The PHP Framework For Web Artisans](https://laravel.com/docs/11.x/blade#stacks)

- [The Power of @stack in Laravel&#39;s Blade - DEV Community](https://dev.to/faridteymouri/the-power-of-stack-in-laravels-blade-4g3b)
