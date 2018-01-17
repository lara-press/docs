# Admin

- [Register Admin Page Routes](#register-admin-page-routes)
- [Register Child Admin Page Routes](#register-child-admin-page-routes)
- [Creating an Admin Controller](#creating-an-admin-controller)

## Register Admin Page Routes

LaraPress allows you to register admin pages in the `routes/web.php`. Use the `adminGet` method to add an admin route. In the second argument, add additional parameters from [`add_menu_page`](https://developer.wordpress.org/reference/functions/add_menu_page/) such as `icon` and `position`. In the example below, the route would be `/cms/wp-admin/admin.php?page=calendar`.


```php
<?php

/** @var LaraPress\Routing\Router $router */

$router->adminGet('calendar', [
    'uses'       => 'AdminCalendarController@index',
    'icon'       => 'dashicons-calendar',
    'position'   => 25,
]);

```

## Register Child Admin Page Routes

Add child admin pages as well. In the second argument, add additional parameters from [`add_submenu_page`](https://developer.wordpress.org/reference/functions/add_submenu_page/). Forward slashes in the `adminGet` URI are converted to dashes for Admin Menu Pages. In the example below, the route would be `/cms/wp-admin/admin.php?page=calendar-settings`. 

```php

$router->adminGet('calendar/settings', [
    'uses'       => 'CalendarController@settings',
]);

```

## Creating an Admin Controller

Admin controllers extend `LaraPress\Admin\AdminPageController`. 


```php
<?php

namespace App\Http\Controllers;

use App\Post;
use LaraPress\Admin\AdminPageController;

class AdminCalendarController extends AdminPageController
{

    public function index()
    {
        return view('admin.calendar.index', [
            'posts' => Post::all(),
        ]);
    }

    public function settings()
    {
        return view('admin.calendar.settings');
    }
```

Note: In our experience, admin pages are most useful when you avoid the "WordPress way". We like to drop in a simple Javascript SPA that can run updates through real endpoints. 
