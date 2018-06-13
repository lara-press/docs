# Metabox

- [Create Metabox](#create-metabox)
- [Use Class Method for inputHandler and outputHandler](#use-class-method-for-inputhandler-andor-outputhandler)
- [Display Metabox on a Post Type](#display-metabox-on-a-post-type)

## Create Metabox
The WordPress [`add_meta_box`](https://developer.wordpress.org/reference/functions/add_meta_box/) function is abstracted with our metabox manager. Instead use the syntax below. Note: `'postType'` takes place of the `add_meta_box` `'screen'` argument.

```php
<?php
        $this->app['metabox']->create([
            'id'            => 'sidebar',
            'title'         => 'Sidebar',
            'context'       => 'side',
            'postType'      => ['page'],
            'inputHandler'  => function ($post, Request $request) {
                $post->setMeta('sidebar', $request->get('sidebar'));
            },
            'outputHandler' => function ($post) {
                return view('metabox.sidebar', [
                    'sidebarOptions' => ['sidebar1' => 'Sidebar 1', 'sidebar2' => 'Sidebar 2'],
                    'post'           => $post,
                ]);
            },
        ]);
```

## Use Class Method for inputHandler and/or outputHandler

```php
            'inputHandler'  => [$this, 'inputHandler'],
            'outputHandler' => [$this, 'outputHandler'],
```

## Display Metabox on a Post Type

Add post type slugs to the `postType` array.

```php
            'postType'      => ['page', 'post', 'project'],
```
