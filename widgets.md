# Widgets

- [Register Widgets](#register-widgets)
- [Define Widgets](#define-widgets)
    - [Save Widget Data](#save-widget-data)
- [Display a Widget](#display-a-widget)

## Register Widgets

Register widgets in the widgets service provider located at `/app/Providers/WidgetServiceProvider`.

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

## Define Widgets

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
            'news' => $this->news,
            'title => get_option('news-widget-title'),
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

#### Save Widget Data

Here is an example of how to save data to a widget. Use the following on a Widget class.

```php

    // Admin Form
    public function form($instance)
    {
        echo view('admin.widgets.news', [
             'name'  => $this->get_field_name('news-widget-title'),
             'value' => get_option('news-widget-title'),
        ]);
    }

    // Admin Form Save
    public function update($newInstance, $oldInstance)
    {
        update_option('news-widget-title', array_get($newInstance, 'news-widget-title'));
    }
```

The `admin.widgets.news` blade file:
```blade
<p>
    <label for="{{ $name }}">Title:</label>
    <input class="widefat" id="{{ $name }}" name="{{ $name }}" value="{{ $value }}" />
</p>
```

## Display a Widget

```blade
@php(the_widget(\App\Widgets\ExampleWidget::class))
```
