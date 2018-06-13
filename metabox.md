# Metabox

## Create Metabox
The WordPress [`add_meta_box`](https://developer.wordpress.org/reference/functions/add_meta_box/) function is abstracted with our metabox manager. Instead use the syntax below. Note: `'postType'` takes place of the `add_meta_box` 'screen'` argument.

```php
<?php
        $this->app['metabox']->create([
            'id'            => 'sidebar',
            'title'         => 'Sidebar',
            'context'       => 'side',
            'postType'      => ['page'],
            'inputHandler'  => [$this, 'inputHandler'],
            'outputHandler' => [$this, 'outputHandler'],
        ]);
```
## Display Metabox on a Post Type

Add post type slugs to the `postType` array.

```php
            'postType'      => ['page', 'post', 'project'],
```