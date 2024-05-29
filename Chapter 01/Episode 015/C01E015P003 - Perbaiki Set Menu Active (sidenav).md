# C01E015P003 - Perbaiki Set Menu Active (sidenav)

app\View\Composers\DashboardComposer.php

```php
use Illuminate\Support\Str;
```

```php
    private function checkMenuActive(&$menu)
    {
        $url = Request::url();
        $active = ($menu['route'] == $url);

        if (isset($menu['withActive']) && $active == false) {
            foreach ($menu['withActive'] as $withActive) {
                $isActive = Str::is($withActive, $url);
                if ($isActive) {
                    $active = $isActive;
                    break;
                }
            }
            unset($menu['withActive']);
        }
        return $active;
    }
```

menus

```php
[
   'title' => 'Tags',
   'icon' => 'bi-tags',
   'route' => route('dashboard.tag'),
   'withActive' => [
      // routes
   ]
]
```
