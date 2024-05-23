## C01E010P002 - Dashboard Provider & View Composer

## Create dashboard provider

```bash
php artisan make:provider DashboardProvider
```

bootstrap\providers.php

```php
<?php

return [
    //..another code
    App\Providers\DashboardProvider::class,
];
```

## Add view composer (dashboard layout)

app\Providers\DashboardProvider.php

```php
<?php

namespace App\Providers;

use Illuminate\Support\Facades\Auth;
use Illuminate\Support\Facades\View as FView;
use Illuminate\Support\ServiceProvider;
use Illuminate\View\View as View;

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
        FView::composer('layouts.dashboard.dashboard-layout', function (View $view) {

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
        });
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
        ];
    }
}

```

## Ref

- https://medium.com/@sunnymalik353/laravel-view-composers-vs-view-creators-a32f117b45c4

- [How to create view composer in Laravel? - Bagisto](https://bagisto.com/en/how-to-create-view-composer-in-laravel/)

- [Views - Laravel 11.x - Passing data to views](https://laravel.com/docs/11.x/views#passing-data-to-views)

- [Views - Laravel 11.x - View composers](https://laravel.com/docs/11.x/views#view-composers)


