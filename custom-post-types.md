# Custom Post Types

- [Creating a Custom Post Type](#create-cpt)
- [Advanced Custom Fields](#acf)

<a name="create-cpt"></a>
## Creating a Custom Post Type

To create a WordPress custom post type, create a class that extends our `Post` class and implements the `CustomPostType` interface. 

The `Post` class is an Eloquent Model. The `CustomPostType` interface requires the `customPostTypeData` method which should return WordPress [`register_post_type`](https://developer.wordpress.org/reference/functions/register_post_type/) function arguments.
 
After the class is created, register it in the PostTypeServiceProvider by adding it to the provider's `$postTypes` array.

Note: When labels are not added as an argument, LaraPress automatically creates both singular and plural labels from the custom post type class name using Laravel helpers. Override these auto created labels with `$singluar` or `$plural` properties on the class.

```php
<?php

namespace App;

use LaraPress\Posts\Post;
use LaraPress\Contracts\Posts\CustomPostType;

class Project extends Post implements CustomPostType
{
    protected $singular = 'LaraPress Project';
    protected $plural = 'LaraPress Projects';

    /**
     * Returns an array of arguments that define the custom post type.
     * These are the same arguments that would normally be passed to register_post_type.
     *
     * @see register_post_type
     * @return array
     */
    public static function customPostTypeData()
    {
        return [
            'supports'            => ['title', 'editor', 'excerpt', 'thumbnail', 'page-attributes'],
            'taxonomies'          => ['category', 'post_tag'],
            'hierarchical'        => false,
            'public'              => true,
            'show_ui'             => true,
            'show_in_menu'        => true,
            'menu_position'       => 25,
            'menu_icon'           => 'dashicons-portfolio',
            'show_in_admin_bar'   => true,
            'show_in_nav_menus'   => true,
            'can_export'          => true,
            'has_archive'         => true,
            'exclude_from_search' => false,
            'publicly_queryable'  => true,
            'capability_type'     => 'page',
            'rewrite'             => ['slug' => 'larapress-projects'],
        ];
    }
}
```

<a name="acf"></a>
## Advanced Custom Fields

One of the best plugins available for WordPress is [Advanced Custom Fields](http://www.advancedcustomfields.com/) by Elliot Condon. LaraPress makes accessing your Advanced Custom Fields meta simple by using the method `getField` on custom post types that extend the `Post` model.

```php
public function getLocation(Project $project)
{
    return $project->getField('location');
}
```
