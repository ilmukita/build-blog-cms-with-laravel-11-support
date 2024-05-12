# C01E001P001 - Setup project Laravel 11

## Create a new Laravel project via Composer's

```bash
composer create-project laravel/laravel=^11.0 blog-ilmukita
```

## Config

### Config App

```bash
APP_NAME=Ilmukita
APP_TIMEZONE="Asia/Jakarta"
```

### Config database

```bash
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=ilmukita_blog
DB_USERNAME=root
DB_PASSWORD=
```

# Migrate Database

```bash
php artisan migrate
```
