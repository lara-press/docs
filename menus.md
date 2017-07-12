# Menu Locations

- [Defining Menu Locations](#menu-locations)
- [Get Menu](#get-menu)

<a name="menu-locations"></a>
## Defining Menu Locations

To add a new menu location, all we have to do is access our menu service provider located at `/app/Providers/MenuServiceProvider.php` and add another element to the property `$menus` array.

```php
<?php namespace App\Providers;

use LaraPress\Menus\MenuServiceProvider as BaseMenuServiceProvider;

class MenuServiceProvider extends BaseMenuServiceProvider
{

    /**
     * An array of id => title pairs to be registered as Wordpress menus.
     *
     * @var array
     */
    protected $menus = [
        'header-nav' => 'Header Navigation',
        'footer-nav' => 'Footer Navigation',
    ];
}
```

## Get Menu

After registering the menu, create and assign a menu in WordPress to it. Then we can access the get that menu's items from `app('menus')`.

```php
    app('menus')->find('header-nav')
```

It returns an array of `MenuItem` objects appropriately nested as defined in WordPress.

*To avoid using [`wp_nav_menu`](https://developer.wordpress.org/reference/functions/wp_nav_menu/) with it's predefined html structure, you can use this.