# Taxonomies

- [Creating a Taxonomy](#creating-a-taxonomy)
- [Register the Taxonomy](#register-the-taxonomy)

## Creating a Taxonomy
To create a custom taxonomy, create a class that implements the `CustomTaxonomy` interface. 

The `CustomTaxonomy` interface requires the `taxonomyData` method which should return WordPress [`register_taxonomy`](https://developer.wordpress.org/reference/functions/register_taxonomy/) function arguments.

```php
<?php namespace App\Taxonomies;

use LaraPress\Contracts\Taxonomies\CustomTaxonomy;

class Category implements CustomTaxonomy 
{

    /**
     * Return an array of arguments that define the custom taxonomy, these
     * are the arguments that would normally be passed to register_taxonomy
     *
     * @see register_taxonomy
     * @return array
     */
    public function taxonomyData()
    {
        return [
            'hierarchical'      => true,
            'public'            => false,
            'show_ui'           => true,
            'show_admin_column' => true,
            'show_in_nav_menus' => false,
            'show_tagcloud'     => true,
        ];
    }

    /**
     * Return an array of post types that this taxonomy supports
     *
     * @see register_taxonomy
     * @return array
     */
    public function supportsPostTypes()
    {
        return ['post'];
    }
}
```

## Register the Taxonomy

After the class is created, register it in the `TaxonomyServiceProvider` by adding it to the provider's `$taxonomies` array.
