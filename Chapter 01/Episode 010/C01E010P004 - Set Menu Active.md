

# C01E010P004 - Set Menu Active

```php
    // use Illuminate\Support\Facades\Request;
    private function generateMenu()
    {
        $menus = $this->getMenus();
        $this->setMenuActive($menus);
        return $menus;
    }
        
    private function setMenuActive(&$menus)
    {
        $setMenuActive = function (&$menu) use (&$setMenuActive) {
            $isActive = false;

            foreach ($menu as &$item) {
                if (isset($item['dropdown'])) {
                    $item['active'] = $setMenuActive($item['dropdown']);
                } else {
                    $item['active'] = ($item['route'] == Request::fullUrl());
                }

                $isActive = $isActive || $item['active'];
            }

            return $isActive;
        };

        foreach ($menus as &$menu) {
            if (isset($menu['menus'])) {
                $setMenuActive($menu['menus']);
            }
        }

        return $menus;
    }
    
    private  function getMenus()
    {
        return [];
    }
```



```php
@isset($menu['dropdown'])
   @php
      $bsTarget = 'collapseLink' . $loop->index;
   @endphp
   <a @class([
       'nav-link',
       'collapsed' => !$menu['active'],
       'active' => $menu['active'],
   ]) href="#" data-bs-toggle="collapse" data-bs-target="#{{ $bsTarget }}"
      aria-expanded="{{ $menu['active'] }}" aria-controls="{{ $bsTarget }}">
      <div class="sb-nav-link-icon">
         <x-icon.bs-icon name="{{ $menu['icon'] }}" />
      </div>
      {{ $menu['title'] }}
      <div class="sb-sidenav-collapse-arrow"><x-icon.bs-icon name="bi-chevron-down" /></div>
   </a>
   <div @class(['collapse', 'show' => $menu['active']]) id="{{ $bsTarget }}" aria-labelledby="{{ $menu['title'] }}"
      data-bs-parent="#sidenavAccordion">
      <nav class="sb-sidenav-menu-nested nav">
         @foreach ($menu['dropdown'] as $dropdown)
            <a @class(['nav-link', 'active' => $dropdown['active']]) href="{{ $dropdown['route'] }}">{{ $dropdown['title'] }}</a>
         @endforeach
      </nav>
   </div>
@else
   <a @class(['nav-link', 'active' => $menu['active']]) href="{{ $menu['route'] }}">
      <div class="sb-nav-link-icon"><x-icon.bs-icon name="{{ $menu['icon'] }}" /></div>
      {{ $menu['title'] }}
   </a>
@endisset

```


