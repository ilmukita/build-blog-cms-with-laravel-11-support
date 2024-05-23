# C01E010P003 - Membuat Class Dashboard Composer

```bash
php artisan make:class App/View/Composers/DashboardComposer
```

app\View\Composers\DashboardComposer.php

```php
<?php

namespace App\View\Composers;

use Illuminate\Support\Facades\Auth;
use Illuminate\View\View;

class DashboardComposer
{
    /**
     * Create a new class instance.
     */
    public function __construct()
    {
        //
    }

    public function compose(View $view): void
    {
        $view->with('app', [
            'name' => config('app.name'),
            'lang' => str_replace('_', '-', app()->getLocale()),
        ]);

        $view->with('user', Auth::user());

        $view->with('route', [
            'dashboard' => route('dashboard.home'),
            'profile' => '/',
            'logout' => route('auth.logout'),
        ]);

        $view->with('sidenavmenu', $this->getMenus());
    }

    private  function getMenus()
    {
        return  [
            [
                'heading' => 'Core',
                'menus' => [
                    [
                        'title' => 'Dashboard',
                        'icon' => 'bi-speedometer2',
                        'route' => route('dashboard.home'),
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
        ];
    }
}
```

app\Providers\DashboardProvider.php

```php
<?php

namespace App\Providers;

use App\View\Composers\DashboardComposer;
use Illuminate\Support\Facades\View as FView;
use Illuminate\Support\ServiceProvider;

class DashboardProvider extends ServiceProvider
{
    /**
     * Register services.
     */
    public function register(): void
    {
        //
    }

    /**
     * Bootstrap services.
     */
    public function boot(): void
    {
        FView::composer('layouts.dashboard.dashboard-layout', DashboardComposer::class);
    }
}
```


