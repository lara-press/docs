#Sidebars

- [Defining Sidebars](#sidebars)

<a name="sidebars"></a>
##Sidebars

Located in `/app/Providers/SidebarServiceProvider.php`, add another entry to the `$sidebars` array.

```php
protected $sidebars = [
    [
        'name'        => 'Example sidebar',
        'description' => 'Just an example sidebar.',
    ],
    [
        'name'        => 'Another sidebar',
        'description' => 'This sidebar is awesome.',
    ],
];
```