# Helpers

- [Available Helpers](#available-helpers)
- [Example](#example)

## Available Helpers

### `actions()`

Returns the `\LaraPress\Actions\Dispatcher` from the service container.

### `assets()`

Returns the `\LaraPress\Assets\Manager` from the service container.

### `filters()`

Returns the `\LaraPress\Filters\Dispatcher` from the service container. 

### `larapress_assets()`

Returns the theme path for `larapress/assets`.

### `post()`

Returns `\LaraPress\Posts\Post` from the service container if exists.

## Example

```php
actions()->listen('admin_enqueue_scripts', function () {
    assets()->enqueueStyle('admin-theme', larapress_assets('/admin/admin.css'));
});
```
