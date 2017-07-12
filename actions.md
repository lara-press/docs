#Actions

- [Using Actions in Service Providers](#actions-in-service-providers)
- [Using Actions with the App Helper Function](#actions-with-app-helper-function)

<a name="actions-in-service-providers"></a>
##Using Actions in Service Providers

We can easily hook into Wordpress's actions, instead of creating a function then calling that function inside of Wordpress's 
`add_action` function, we simply access it through the service container and use a callback. Let's say we've created a service 
provider specifically for theme functions and we're going to use one of our installed plugins functions. In this case, we're 
going to want to make sure our plugins are loaded before we can access their functions using the `plugins_loaded` Wordpress 
action.

```php
<?php namespace App\Providers;

use Illuminate\Support\ServiceProvider;

class ThemeFunctionsServiceProvider extends ServiceProvider
{

    public function register()
    {
        actions()->listen('plugins_loaded', function() {
            //Code goes here
        });
    }
}
```

<a name="actions-with-app-helper-function"></a>
##Using Actions with the App Helper Function

Of course you can also hook into the Wordpress actions using the app helper function.

```php
app('actions')->listen('plugins_loaded', function() {
    //Code goes here
});
```