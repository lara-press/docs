# Filters

- [Using Filters in Service Providers](#filters-in-service-providers)
- [Using Filters with the App Helper Function](#filters-with-app-helper-function)

<a name="filters-in-service-providers"></a>
## Using Filters in Service Providers

Easily hook into Wordpress's filters. 

Instead of creating a function then calling that function inside of Wordpress's [`add_filter`](https://developer.wordpress.org/reference/functions/add_filter/) function, simply access it through the service container and use a callback. 

Let's say we've created a service provider specifically for theme functions. We'll filter `the_content` output by using the `the_content` filter.  

```php
<?php namespace App\Providers;

use Illuminate\Support\ServiceProvider;

class ThemeFunctionsServiceProvider extends ServiceProvider
{
    public function register()
    {
        $this->app['actions']->listen('the_content', function($content) {
            
            if (is_single()) {
                $content = sprintf(
                    '<img class="banner" src="%s/images/banner.png" alt="Banner Image" />%s',
                    larapress_assets(),
                    $content
                );
            }
            
            return $content;
        });
    }
}
```

<a name="filters-with-app-helper-function"></a>
## Using Filters with the App Helper Function

Of course you can also hook into Wordpress filters using the app helper function.

```php
app('filters')->listen('the_content', function($content) {
    //Code goes here
});
```