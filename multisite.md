# Multisite

Note: Only supports subdomain install

- [Register Service Provider](#register-service-provider)
- [Follow WordPress Instructions](#follow-wordpress-instructions)

## Register Service Provider

To add Multisite support to LaraPress, register the MultisiteServiceProvider in your app.php config file.

```php
    LaraPress\Multisite\MultisiteServiceProvider::class,
```

## Follow WordPress Instructions

Found the instructions from [WordPress](https://codex.wordpress.org/Create_A_Network).
