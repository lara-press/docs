# Routing

- [Handle Method](#handle-method)
    - [Use Custom Types From A Plugin](#use-custom-types-from-a-plugin)
- [Admin Routes](#admin-routes)

## Handle Method

Use the handle method for Custom Post Types routes. It can handle all routes for Pages, Posts, or any Custom Post Types created in WP Admin. Note: The handle will only work if the Model is registered in the `PostTypeServiceProvider`

```php
/** @var LaraPress\Routing\Router $router */

$router->handle(\App\Page::class, 'PageController@handle');
$router->handle(\App\Post::class, 'PostController@handle');
$router->handle(\App\News::class, 'NewsController@handle');
```

With the handle method, you don't need to statically register each route.

#### Use Custom Types From A Plugin

Some plugins use custom post types. Create a custom post type from the custom post type's `post_type` with a TitleCased class name. The model should extend `Post.php` or the Eloquent Model.

For [The Events Calendar's](https://theeventscalendar.com/) event custom post type, the event `post_type` is "tribe_events". The model would be named TribeEvents.

After that, you can register the route.

 ```php
 $router->handle(\App\TribeEvents::class, 'EventController@handle');
 ```
 
## Admin Panel Routes
 
Define [Admin Pages](https://github.com/lara-press/docs/blob/master/admin.md) in a controller. Use WordPress actions and filters to manage other admin routes.
