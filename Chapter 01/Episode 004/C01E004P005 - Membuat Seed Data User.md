# C01E004P004 - Membuat Seed Data User

## Make seed data

```bash
 php artisan make:seed UserTableSeeder
```

database\seeders\UserTableSeeder.php

```php
<?php

namespace Database\Seeders;

use Illuminate\Database\Console\Seeds\WithoutModelEvents;
use Illuminate\Database\Seeder;
use App\Models\User;

class UserTableSeeder extends Seeder
{
    /**
     * Run the database seeds.
     */
    public function run(): void
    {
        User::factory()->create([
            'name' => 'ilmukita',
            'email' => 'ilmukita@mail.test',
        ]);
    }
}
```

database\seeders\DatabaseSeeder.php

```php
<?php

namespace Database\Seeders;


// use Illuminate\Database\Console\Seeds\WithoutModelEvents;
use Illuminate\Database\Seeder;

class DatabaseSeeder extends Seeder
{
    /**
     * Seed the application's database.
     */
    public function run(): void
    {
        $this->call([
            UserTableSeeder::class
        ]);
    }
}
```

## Running Seeders

```bash
php artisan db:seed

#by class
php artisan db:seed --class=UserTableSeeder
```

## Migrate Data + Seed Data

```php
php artisan migrate:fresh --seed
```

## Ref

- https://laravel.com/docs/11.x/seeding
