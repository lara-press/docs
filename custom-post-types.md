# Custom Post Types

- [Creating a Custom Post Type](#creating-a-custom-post-type)
- [Manage Admin Page Columns](#manage-admin-page-columns)
- [Advanced Custom Fields](#advanced-custom-fields)

## Creating a Custom Post Type

To create a WordPress custom post type, create a class that extends our `Post` class and implements the `CustomPostType` interface. 

The `Post` class is an Eloquent Model. The `CustomPostType` interface requires the `customPostTypeData` method which should return WordPress [`register_post_type`](https://developer.wordpress.org/reference/functions/register_post_type/) function arguments.
 
After the class is created, register it in the PostTypeServiceProvider by adding it to the provider's `$postTypes` array.

See the [Routing](https://github.com/lara-press/docs/blob/master/routing.md#handle-method) docs for handling `CustomPostType` routes.

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

## Manage Admin Page Columns

A `getAdminColumns` method allows Admin Page Columns to be added or removed. Add columns by assigning keys to the Column class. Remove columns by assigning keys to false.

The Column class is constructed with two arguments. The first is a column Label. The second is optional to allow use of native columns like "author"; it can be null, a value or a callback. If a callback is used, the first callback parameter is `$postId`.

```php
    public static function getAdminColumns()
    {
        return [
            'author'    => new Column('Author'),
            'location'  => new Column('Location', function ($postId) {
                return get_field('location', $postId);
            }),
            'thumbnail' => new Column('Thumbnail', function ($postId) {
                return wp_get_attachment_image(get_post_thumbnail_id($postId));
            }),
            'date'      => false,
        ];
    }
```

## Advanced Custom Fields

One of the best plugins available for WordPress is [Advanced Custom Fields](http://www.advancedcustomfields.com/) by Elliot Condon. LaraPress makes accessing your Advanced Custom Fields meta simple by using the method `getField` on custom post types that extend the `Post` model.

```php
public function getLocation(Project $project)
{
    return $project->getField('location');
}
```
