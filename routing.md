# Routing

- [Handle Method](#handle-method)
- [Admin Routes](#admin-routes)

## Handle Method

Use the handle method for Custom Post Types routes. It can handle all routes for Pages, Posts, or any Custom Post Types created in WP Admin. Note: The handle will only work if the Model is registered in the `PostTypeServiceProvider`

```php
/** @var LaraPress\Routing\Router $router */

$router->handle(\App\Page::class, 'PageController@single');
$router->handle(\App\Post::class, 'PostController@single');
$router->handle(\App\News::class, 'NewsController@single');
```

With the handle method, you don't need to statically register each route.

## Admin Panel Routes

Defined [Admin Pages](https://github.com/lara-press/docs/blob/master/admin.md) in a controller. Use WordPress actions and filters to manage other admin routes.
