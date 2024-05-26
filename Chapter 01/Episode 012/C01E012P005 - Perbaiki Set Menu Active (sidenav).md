# C01E012P005 - Perbaiki Set Menu Active (sidenav)

app\View\Composers\DashboardComposer.php

```php
$item['active'] = ($item['route'] == Request::fullUrl());
// to
$item['active'] = ($item['route'] == Request::url());
```


