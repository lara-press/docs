# Custom Post Types

- [Creating a Custom Post Type](#create-cpt)
- [Advanced Custom Fields](#acf)

<a name="create-cpt"></a>
## Creating a Custom Post Type

To create a Wordpress custom post type, we need to create a new class under `/app` that extends our `Post` class and implements 
the `CustomPostType` interface. Our post class is an Eloquent ORM so you'll have access to all of it's functionality. When 
implementing the `CustomPostType` interface you'll be required to include the `customPostTypeData` method, this is where
all of your arguments from the `register_post_type` Wordpress function will be. If the labels array is not added as an argument,
LaraPress will handle them automatically by creating a singular and plural label from the post type class name using Laravel 
helpers, if you would like to override these auto created labels simply add the properties `$singluar` or `$plural` to the class.

```php
<?php namespace App;

use LaraPress\Contracts\Posts\CustomPostType;

class Project extends Model implements CustomPostType
{
    protected $singular = 'Larapress Project';
    protected $plural = 'Larapress Projects';

    /**
     * Returns an array of arguments that define the custom post type. 
     * These are the same arguments that would normally be passed to register_post_type.
     *
     * @see register_post_type
     * @return array
     */
    public function customPostTypeData()
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
            'rewrite'             => ['slug' => 'larapress-projects']
        ];
    }
}
```

<a name="acf"></a>
## Advanced Custom Fields

One of the best plugins available for WordPress is [Advanced Custom Fields](http://www.advancedcustomfields.com/),
by Elliot Condon. LaraPress makes accessing your Advanced Custom Fields meta simple by using the method `getField` which 
we have access to when we extended the `Post` model.

```php
public function single($slug, Project $projects)
{
    $project = $projects->findByName($slug);

    $location = $project->getField('location');
    
    return view('pages.project-single', ['location' => $location])
}
```
