#Menu Locations

- [Defining Menu Locations](#menu-locations)

<a name="menu-locations"></a>
##Defining Menu Locations

To add a new menu location, all we have to do is access our menu service provider located at `/app/Providers/MenuServiceProvider.php`, 
and add another element to the property `$menus` array.

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