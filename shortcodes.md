# Shortcodes

- [Creating a Shortcode](#creating-a-shortcode)
- [Shortcode Views](#shortcode-views)

## Creating a Shortcode

To create a WordPress shortcode, add the shortcode name to the `$shortcodes` array in the ShortcodeServiceProvider.

It first checks for a method, then it checks for a view. 

A shortcode method should use start with the shortocde name as camelCase followed by 'Shortcode'. If my shortcode is named 'hello-world', then the method would be `helloWorldShortcode`.

A view should be placed in the `views/shortcodes` folder named after the shortcode. If my shortcode is named 'fancy-title', then the view would be `fancy-title.blade.php`. 

```php
<?php

namespace App\Providers;

use LaraPress\Shortcodes\ShortcodeServiceProvider as BaseShortcodeServiceProvider;

class ShortcodeServiceProvider extends BaseShortcodeServiceProvider
{
    protected $shortcodes = [
        'hello-world',
        'fancy-title',
    ];

    public function helloWorldShortcode()
    {
        return 'Hello world!';
    }
}
```

## Shortcode Views
    
After registering `fancy-title` as a shortcode, create a view named `fancy-title.blade.php` in the `views/shortcodes` folder.

```blade
<h3 class="{{ array_get($attributes, 'animation') }}">{{ $content }}</h3>
```

A shortcode view has an `$attributes` array and a `$content` variable available.

After the view is ready, you can use the shortcode in the WordPress content area.

    [fancy-title animation="wave"]