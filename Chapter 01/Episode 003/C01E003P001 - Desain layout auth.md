# C01E003P001 - Desain Layout Auth

## File SASS

resources\sass\layout\auth\_auth.scss

```sass
//
// Authentication layout
//

#layoutAuthentication {
    display: flex;
    flex-direction: column;
    min-height: 100vh;

    #layoutAuthentication_content {
        min-width: 0;
        flex-grow: 1;
    }

    #layoutAuthentication_footer {
        min-width: 0;
    }
}

```

resources\sass\_layouts.scss

```sass
@import "./layout/auth/auth";
```

resources\sass\app.scss

```sass
// @import "./components";

@import "./layouts";

// @import "./helpers";
```

## Layout Auth

resources\views\layouts\auth\auth-layout.blade.php

```html
<body class="bg-primary">
   <div id="layoutAuthentication">
      <div id="layoutAuthentication_content">
         <main>
            {{-- content --}}
         </main>
      </div>
      {{-- footer --}}
   </div>

   {{-- js --}}
</body>
```

resources\views\layouts\auth\_footer.blade.php

```html
<div id="layoutAuthentication_footer">
   <footer class="py-4 bg-light mt-auto">
      <div class="container-fluid px-4">
         <div class="d-flex align-items-center justify-content-between small">
            <div class="text-muted">Copyright &#169; Your website</div>
         </div>
      </div>
   </footer>
</div>
```

## Ref

- SB Admin [A Bootstrap 5 admin template]([Start Bootstrap](https://startbootstrap.com/template/sb-admin#google_vignette)

- SASS lang [sass-lang](https://sass-lang.com/)

- @include [including-subviews](https://laravel.com/docs/11.x/blade#including-subviews)
