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

## Define DB_TABLE PREFIX for LaraPress multisite

Open your wp-config file.

Change the 

`define('DB_TABLE_PREFIX', $table_prefix = env('DB_TABLE_PREFIX', 'wp_'));`

to

`$table_prefix = 'wp_';`

Below `require_once(ABSPATH . 'wp-settings.php');`, add the following. This adds the correct prefix for LaraPress queries.

```php
// define table prefix for larapress
global $wpdb;

define('DB_TABLE_PREFIX', $wpdb->prefix);
```
