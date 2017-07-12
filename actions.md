# Actions

- [Using Actions in Service Providers](#actions-in-service-providers)
- [Using Actions with the App Helper Function](#actions-with-app-helper-function)

<a name="actions-in-service-providers"></a>
## Using Actions in Service Providers

Easily hook into Wordpress's actions.

Instead of creating a function then calling that function inside of Wordpress's [`add_action`](https://developer.wordpress.org/reference/functions/add_action/) function, simply access it through the service container and use a callback. 

Let's say we've created a service provider specifically for theme functions. We'll send an email on `save_post`.

```php
<?php namespace App\Providers;

use Illuminate\Mail\Message;
use Illuminate\Support\ServiceProvider;

class ThemeFunctionsServiceProvider extends ServiceProvider
{

    public function register()
    {
        $this->app['actions']->listen('save_post', function($id, $post) {
            app('mailer')->send('emails.saved_post', $post, function(Message $message) {
                $message->from('no-reply@example.com');
                $message->to('admin@example.com');
                $message->subject('Post was saved');
            });
        });
    }
}
```

<a name="actions-with-app-helper-function"></a>
## Using Actions with the App Helper Function

Of course you can also hook into Wordpress actions using the app helper function.

```php
app('actions')->listen('save_post', function() {
    //Code goes here
});
```