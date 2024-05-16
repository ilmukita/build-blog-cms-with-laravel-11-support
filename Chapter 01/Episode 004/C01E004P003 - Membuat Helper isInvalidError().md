# C01E004P003 - Membuat Helper isInvalidError()

## Membuat Helper

app\Support\helpers.php

```php
<?php


if (!function_exists('isInvalidError')) {
    function isInvalidError($fieldName, $errorBag = null)
    {
        $errors = session()->get('errors');

        if ($errors && $errors->has($fieldName)) {
            if ($errorBag) {
                return $errors->getBag($errorBag)->has($fieldName);
            }
            return true;
        }

        return false;
    }
}
```

composer.json

```json
    "autoload": {        
        "files": [
            "./app/Support/helpers.php"
        ]
    },
```

```bash
composer dump-autoload
```

## Use

```php
@class(['is-invalid' => isInvalidError('keyName')])
```

## Ref

- [Creating Your Own PHP Helpers in a Laravel Project - Laravel News](https://laravel-news.com/creating-helpers)

- https://laravel.com/docs/11.x/blade#conditional-classes
