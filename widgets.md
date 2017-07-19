# Widgets

- [Defining Widgets](#defining-widgets)
- [Registering Widgets](#registering-widgets)

<a name="defining-widgets"></a>
## Defining Widgets

Create a widget class in `/app/Widgets`. It looks very similar to the [WordPress format](https://codex.wordpress.org/Widgets_API) except we extend our own widget class. From here, if you want to return a view you must `echo` it.

*Note: Leaving empty form and update methods can break the widget*

```php
<?php namespace App\Widgets;

use App\News;
use LaraPress\Widgets\Widget;

class ExampleWidget extends Widget
{

    protected $news;

    function __construct()
    {
        parent::__construct(class_basename($this), 'News Widget');
        $this->news = News::all();
    }

    // Output
    function widget($args, $instance)
    {
        echo view('widgets.news', array(
            'news' => $this->news
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
     * An array of class names to be registered as WordPress widgets.
     *
     * @var array
     */
    protected $widgets = [
        'App\Widgets\ExampleWidget'
    ];
}
```