# C01E007P001 - Desain Layout Dashboard

## Config SASS

resources\sass\_layouts.scss

```sass
@import "./layout/dashboard/dashboard";
```

resources\sass\_variables.scss

```sass
//
// Variables
//

// Import Bootstrap variables for use within theme
@import "bootstrap/scss/variables";
@import "bootstrap/scss/variables-dark";

@import "./layout/dashboard/variables/spacing.scss";
@import "./layout/dashboard/variables/navigation.scss";
```

## Template Layout Dashboard

### Main Layout

```php
<body class="sb-nav-fixed">
   {{-- navbar --}}
   <div id="layoutSidenav">
      <div id="layoutSidenav_nav">
         {{-- sidenav --}}
      </div>
      <div id="layoutSidenav_content">
         <main>
            <div class="container-fluid px-4">
               <h1 class="mt-4">
                  {{-- title --}}
               </h1>
               {{-- bread/content --}}
            </div>
         </main>
         {{-- footer --}}
      </div>
   </div>
   {{-- script/js --}}
</body>
```

### Navbar

```php
<nav class="sb-topnav navbar navbar-expand navbar-dark bg-dark">
   <!-- Navbar Brand-->
   <a class="navbar-brand ps-3" href="/">App name</a>
   <!-- Sidebar Toggle-->
   <button class="btn btn-link btn-sm order-1 order-lg-0 me-4 me-lg-0" id="sidebarToggle" href="#!"><i
         class="bi bi-list"></i></button>
   <!-- Navbar-->
   <ul class="navbar-nav ms-auto me-3 me-lg-4">
      <li class="nav-item dropdown">
         <a class="nav-link dropdown-toggle" id="navbarDropdown" href="#" role="button" data-bs-toggle="dropdown"
            aria-expanded="true"><i class="bi bi-person"></i></a>
         <ul class="dropdown-menu dropdown-menu-end" aria-labelledby="navbarDropdown" data-bs-popper="static">
            <li><a class="dropdown-item" href="/">Profile</a></li>
            <li>
               <hr class="dropdown-divider">
            </li>
            <li><a id="actionLogout" class="dropdown-item" href="#">Logout</a></li>
         </ul>
      </li>
   </ul>
</nav>
```

### Sidenav

```php
<nav class="sb-sidenav accordion sb-sidenav-dark" id="sidenavAccordion">
   <div class="sb-sidenav-menu">
      <div class="nav">
         <div class="sb-sidenav-menu-heading">Core</div>
         <a class="nav-link" href="/">
            <div class="sb-nav-link-icon"><i class="bi bi-speedometer2"></i></div>
            Dashboard
         </a>
         <div class="sb-sidenav-menu-heading">Dropdown</div>
         <a class="nav-link collapsed" href="#" data-bs-toggle="collapse" data-bs-target="#collapseLink1"
            aria-expanded="false" aria-controls="collapseLink1">
            <div class="sb-nav-link-icon"><i class="bi bi-share"></i></div>
            Link 1
            <div class="sb-sidenav-collapse-arrow"><i class="bi bi-chevron-down"></i></div>
         </a>
         <div class="collapse" id="collapseLink1" aria-labelledby="headingOne" data-bs-parent="#sidenavAccordion">
            <nav class="sb-sidenav-menu-nested nav">
               <a class="nav-link" href="/">Link 1.1</a>
               <a class="nav-link" href="/">Link 1.2</a>
            </nav>
         </div>
         <a class="nav-link collapsed" href="#" data-bs-toggle="collapse" data-bs-target="#collapseLink2"
            aria-expanded="false" aria-controls="collapseLink2">
            <div class="sb-nav-link-icon"><i class="bi bi-share"></i></div>
            Link 2
            <div class="sb-sidenav-collapse-arrow"><i class="bi bi-chevron-down"></i></div>
         </a>
         <div class="collapse" id="collapseLink2" aria-labelledby="headingOne" data-bs-parent="#sidenavAccordion">
            <nav class="sb-sidenav-menu-nested nav">
               <a class="nav-link" href="/">Link 2.1</a>
               <a class="nav-link" href="/">Link 2.2</a>
            </nav>
         </div>
         <a class="nav-link" href="/">
            <div class="sb-nav-link-icon"><i class="bi bi-share"></i></div>
            Link 3
         </a>
      </div>
   </div>
   <div class="sb-sidenav-footer">
      <div class="small">Logged in as:</div>
      Start Bootstrap
   </div>
</nav>
```

### Footer

```php
<footer class="py-4 bg-light mt-auto">
   <div class="container-fluid px-4">
      <div class="d-flex align-items-center justify-content-between small">
         <div class="text-muted">Copyright © Your Website</div>
      </div>
   </div>
</footer>
```

### Breadcrumb

```php
<nav aria-label="breadcrumb">
   <ol class="breadcrumb">
      <li class="breadcrumb-item"><a href="#">Home</a></li>
      <li class="breadcrumb-item"><a href="#">Library</a></li>
      <li class="breadcrumb-item active" aria-current="page">Data</li>
   </ol>
</nav>
```

## Ref

- [GitHub - StartBootstrap/startbootstrap-sb-admin: A free, open source, Bootstrap admin theme created by Start Bootstrap](https://github.com/StartBootstrap/startbootstrap-sb-admin)
