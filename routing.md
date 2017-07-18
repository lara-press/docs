# Routing

- [Handle Method](#handle-method)

## Handle Method

Use the handle method for Custom Post Types routes. It can handle all routes for Pages, Posts, or any Custom Post Types created in WP Admin.

```php
/** @var LaraPress\Routing\Router $router */

$router->handle(\App\Page::class, 'PageController@single');
$router->handle(\App\Post::class, 'PostController@single');
$router->handle(\App\News::class, 'NewsController@single');
```

With the handle method, you don't need to statically register each route.
