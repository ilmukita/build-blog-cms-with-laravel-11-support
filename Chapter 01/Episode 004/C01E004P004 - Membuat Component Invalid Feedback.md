# C01E004P004 - Membuat Component Invalid Feedback

## Create component

```php
 php artisan make:component Error/InvalidFeedback
```

app\View\Components\Error\InvalidFeedback.php

```php
<?php

namespace App\View\Components\Error;

use Closure;
use Illuminate\Contracts\View\View;
use Illuminate\View\Component;

class InvalidFeedback extends Component
{
    /**
     * Create a new component instance.
     */
    public function __construct(public string $fieldName)
    {
    }

    public function shouldRender()
    {
        return isset($this->fieldName);
    }

    /**
     * Get the view / contents that represent the component.
     */
    public function render(): View|Closure|string
    {
        return view('components.error.invalid-feedback');
    }
}
```

resources\views\components\error\invalid-feedback.blade.php

```php
@error($fieldName)
   <div class="invalid-feedback">{{ $message }}</div>
@enderror
```

## Use

```php
<x-error.invalid-feedback fieldName="email" />
```

## Ref

- [Blade Templates - Laravel 11.x - The PHP Framework For Web Artisans](https://laravel.com/docs/11.x/blade#components)
