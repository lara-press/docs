# Widgets

- [Defining Widgets](#defining-widgets)
- [Registering Widgets](#registering-widgets)

<a name="defining-widgets"></a>
## Defining Widgets

Create the widget class at '/app/Widgets', which will look similar to Wordpress's format except we extend our own widget 
class. From here, if you want to return a view you must `echo` it.

*Note: Leaving empty form and update methods can break the widget*

```php
<?php namespace App\Widgets;

use LaraPress\Widgets\Widget;

class ExampleWidget extends Widget
{

    protected $recentNews;

    function __construct(News $news)
    {
        parent::__construct(false, 'Example Widget');
        $this->recentNews = $news->getRecentNews();
    }

    // Output
    function widget($args, $instance)
    {
        echo view('widgets.example-widget', array(
            'recent-posts' => $this->recentPosts
        ));
    }

    // Admin Form
    public function form($instance)
    {
    }

    // Admin Form Save
    public function update($new_instance, $old_instance)
    {
    }
}
```

<a name="registering-widgets"></a>
## Registering Widgets

Next we'll need to register our widget the in the widgets service provider located at `/app/Providers/WidgetServiceProvider`.

```php
<?php namespace App\Providers;

use LaraPress\Widgets\WidgetServiceProvider as BaseWidgetServiceProvider;

class WidgetServiceProvider extends BaseWidgetServiceProvider
{

    /**
     * An array of class names to be registered as Wordpress widgets.
     *
     * @var array
     */
    protected $widgets = [
        'App\Widgets\ExampleWidget'
    ];
}
```