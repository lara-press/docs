#Custom Post Types

- [Creating a Custom Post Type](#create-cpt)
- [Advanced Custom Fields](#acf)

<a name="create-cpt"></a>
##Create a Custom Post Type

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse convallis, 
sem a ultricies porttitor, metus velit hendrerit erat, id vulputate nulla mauris 
eget tortor.

```php
class Project extends Model implements CustomPostType
{
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
            'rewrite' => ['slug' => 'project'],
            'supports' => array('title', 'editor', 'thumbnail'),
        ];
    }
}
```

<a name="acf"></a>
##Advanced Custom Fields

One of the best plugins available for WordPress is [Advanced Custom Fields](http://www.advancedcustomfields.com/),
by Elliot Condon. LaraPress makes accessing your custom fields simple.

```php
$location = $project->getField('location');

```
