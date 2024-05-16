# C01E004P002 - Validasi Form Login

## Validate

```php
$request->validate(['email' => ['required', 'string', 'email'], 'password' => ['required', 'string', ]]);       ]);
```

## Show error

```php
class="form-control @error('errorName') is-invalid @enderror"
```

```php
@error('errorName')
   <div class="invalid-feedback">{{ $message }}</div>
@enderror
```

# Ref

- [Writing the Validation Logic](https://laravel.com/docs/11.x/validation#quick-writing-the-validation-logic)

- [Old input](https://laravel.com/docs/11.x/requests#old-input)

- [Validation errors](https://laravel.com/docs/11.x/blade#validation-errors)

- [Laravel old method not returning password values]([php - Laravel old method not returning password values - Stack Overflow](https://stackoverflow.com/questions/55813487/laravel-old-method-not-returning-password-values))

- [The old() helper is not working with passwords](https://laracasts.com/discuss/channels/laravel/the-old-helper-is-not-working-with-passwords)
