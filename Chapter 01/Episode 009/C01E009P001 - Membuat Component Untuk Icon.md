# C01E009P001 - Membuat Component Untuk Icon

## Create Icon Component

```bash
 php artisan make:component Icon/BsIcon
```

app\View\Components\Icon\BsIcon.php

```php
<?php

namespace App\View\Components\Icon;

use Closure;
use Illuminate\Contracts\View\View;
use Illuminate\View\Component;

class BsIcon extends Component
{
    public function __construct(
        public string $name
    ) {
        //
    }

    public function shouldRender()
    {
        return isset($this->name);
    }

    public function render(): View|Closure|string
    {
        return view('components.icon.bs-icon');
    }
}


```

resources\views\components\icon\bs-icon.blade.php

```php
<i @class(['bi', $name])></i>
```

## Use

```php
<x-icon.bs-icon name="icon-name" />
```

## Ref

- https://laravel.com/docs/11.x/blade#components
