#Sidebars

- [Defining Sidebars](#defining-sidebars)

<a name="defining-sidebars"></a>
##Defining Sidebars

To add a new sidebar, all we have to do is access our sidebar service provider located at `/app/Providers/SidebarServiceProvider.php`, 
and add another element to the property `$sidebars` array.

```php
<?php namespace App\Providers;

use LaraPress\Sidebars\SidebarServiceProvider as BaseSidebarServiceProvider;

class SidebarServiceProvider extends BaseSidebarServiceProvider
{

    /**
     * An array of sidebars to be loaded as Wordpress sidebars.
     *
     * @see LaraPress\Sidebars\SidebarServiceProvider for proper structure
     * @var array
     */
    protected $sidebars = [
        [
            'name'        => 'Example sidebar',
            'description' => 'Just an example sidebar',
        ],
        [
            'name'        => 'Another Sidebar',
            'description' => 'This is just another sidebar'
        ]
    ];
}
```