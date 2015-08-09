#Menus

- [Defining Menu Locations](#menu-locations)

<a name="menu-locations"></a>
##Defining Menu Locations

Located in `/app/Providers/MenuServiceProvider.php`, add another entry to the `$menus` array.

```php
protected $menus = [
    'header-nav' => 'Header Navigation',
    'footer-nav' => 'Footer Navigation',
];
```