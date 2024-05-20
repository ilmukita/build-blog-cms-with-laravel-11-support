# C01E007P004 - Menampilkan Username dan App Name



resources\views\layouts\dashboard\dashboard-layout.blade.php

```php
@php
   $app = [
       'name' => config('app.name'),
       'lang' => str_replace('_', '-', app()->getLocale()),
   ];
   $user = auth()->user();
   $route = [
       'dashboard' => route('dashboard.home'),
       'profile' => '/',
       'logout' => route('auth.logout'),
   ];
@endphp
```

```php
// resources\views\layouts\dashboard\_navbar.blade.php
   <!-- Navbar Brand-->
   <a class="navbar-brand ps-3" href="{{ $route['dashboard'] }}">{{ $app['name'] }}</a>
   <!-- navbarDropdown -->
   <ul class="dropdown-menu dropdown-menu-end" aria-labelledby="navbarDropdown" data-bs-popper="static">
      <li><a class="dropdown-item" href="{{ $route['profile'] }}">Profile</a></li>
      <li>
         <hr class="dropdown-divider">
      </li>
      <li><a id="actionLogout" class="dropdown-item" href="#">Logout</a></li>
      <form id="formLogin" action="{{ $route['logout'] }}" method="POST">
         @csrf
      </form>
   </ul>
// resources\views\layouts\dashboard\_sidenav.blade.php
<div class="sb-sidenav-footer">
   <div class="small">Logged in as:</div>
   {{ $user['email'] }}
</div>

// resources\views\layouts\dashboard\_footer.blade.php
<div class="text-muted">Copyright © {{ $app['name'] }}</div>
```


