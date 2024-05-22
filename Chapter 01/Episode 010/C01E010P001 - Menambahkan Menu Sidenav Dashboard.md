# C01E010P001 - Menambahkan Menu Sidenav Dashboard

## Menu Template

```php
[
       [
           'heading' => 'Core',
           'menus' => [
               [
                   'title' => 'Dashboard',
                   'icon' => 'bi-speedometer2',
                   'route' => '/',
               ],
           ],
       ],
       [
           'heading' => 'Dropdown',
           'menus' => [
               [
                   'title' => 'Link 1',
                   'icon' => 'bi-share',
                   'dropdown' => [
                       [
                           'title' => 'Link 1.1',
                           'route' => '/',
                       ],
                       [
                           'title' => 'Link 1.2',
                           'route' => '/',
                       ],
                   ],
               ],
               [
                   'title' => 'Link 2',
                   'icon' => 'bi-share',
                   'dropdown' => [
                       [
                           'title' => 'Link 2.1',
                           'route' => '/',
                       ],
                       [
                           'title' => 'Link 2.2',
                           'route' => '/',
                       ],
                   ],
               ],
               [
                   'title' => 'Link 3',
                   'icon' => 'bi-share',
                   'route' => '/',
               ],
           ],
       ],
   ]
```

resources\views\layouts\dashboard\_sidenav.blade.php

```php
@foreach ($sidenavmenu as $menus)
   @foreach ($menus as $key => $value)
      @if ($key == 'heading')
         <div class="sb-sidenav-menu-heading">
            {{ $value }}
         </div>
      @endif

      @if ($key == 'menus')
         @foreach ($value as $menu)
            @isset($menu['dropdown'])
               @php
                  $databstarget = 'collapseLink' . $loop->index + 1;
               @endphp
               <a class="nav-link collapsed" href="#" data-bs-toggle="collapse" data-bs-target="#{{ $databstarget }}"
                  aria-expanded="false" aria-controls="{{ $databstarget }}">
                  <div class="sb-nav-link-icon">
                     <x-icon.bs-icon name="{{ $menu['icon'] }}" />
                  </div>
                  {{ $menu['title'] }}
                  <div class="sb-sidenav-collapse-arrow">
                     <x-icon.bs-icon name="bi-chevron-down" />
                  </div>
               </a>

               <div class="collapse" id="{{ $databstarget }}" aria-labelledby="{{ $menu['title'] }}"
                  data-bs-parent="#sidenavAccordion">
                  <nav class="sb-sidenav-menu-nested nav">
                     @foreach ($menu['dropdown'] as $dropdown)
                        <a class="nav-link" href="{{ $dropdown['route'] }}">
                           {{ $dropdown['title'] }}
                        </a>
                     @endforeach
                  </nav>
               </div>
            @else
               <a class="nav-link" href="{{ $menu['route'] }}">
                  <div class="sb-nav-link-icon">
                     <x-icon.bs-icon name="{{ $menu['icon'] }}" />
                  </div>
                  {{ $menu['title'] }}
               </a>
            @endisset
         @endforeach
      @endif
   @endforeach
@endforeach

```

# Ref

- [Blade Templates - Laravel 11.x - The PHP Framework For Web Artisans](https://laravel.com/docs/11.x/blade#blade-directives)

- [Blade Templates - Laravel 11.x - The PHP Framework For Web Artisans](https://laravel.com/docs/11.x/blade#the-loop-variable)
