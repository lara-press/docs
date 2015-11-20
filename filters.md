#Filters

- [Using Filters in Service Providers](#filters-in-service-providers)
- [Using Filters with the App Helper Function](#filters-with-app-helper-function)

<a name="filters-in-service-providers"></a>
##Using Filters in Service Providers

We can easily hook into Wordpress's filters, instead of creating a function then calling that function inside of Wordpress's 
`add_filter` function, we simply access it through the service container and use a callback. Let's say we've created a service 
provider specifically for theme functions and we're going to filter `the_content` output, we'll use the `the_content` filter.  

```php
<?php namespace App\Providers;

use Illuminate\Support\ServiceProvider;

class ThemeFunctionsServiceProvider extends ServiceProvider
{
    public function register()
    {
        $this->app['filters']->listen('the_content', function() {
            //Code goes here
        });
    }
}
```

<a name="filters-with-app-helper-function"></a>
##Using Filters with the App Helper Function

Of course you can also hook into the Wordpress filters using the app helper function.

```php
app('filters')->listen('the_content', function() {
    //Code goes here
});
```