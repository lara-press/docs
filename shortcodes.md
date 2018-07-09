# Shortcodes

- [Create a Simple Shortcode](#create-a-simple-shortcode)
- [Create a Dynamic Shortcode](#create-a-dynamic-shortcode)

There are 2 ways to create shortcodes.

## Create a Simple Shortcode

To create a simple WordPress shortcode, add a shortcode name to the `$shortcodes` array in the ShortcodeServiceProvider.

A shortcode is rendered from a method on the ShortcodeServiceProvider or a view in the `shortcodes` folder. The priority is the method.

A method on the ShortcodeServiceProvider starts the shortcode name in camelCase followed by 'Shortcode'. If my shortcode is named 'hello-world', then the method would be `helloWorldShortcode`.

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
    
A view should be placed in the `shortcodes` view folder named after the shortcode. If my shortcode is named 'fancy-title', then the view would be `fancy-title.blade.php`. 

If you register `fancy-title` as a shortcode, then create a view named `fancy-title.blade.php` in the `shortcodes` view folder.

A shortcode view has an `$attributes` array and a `$content` variable available.

```blade
<h3 class="{{ array_get($attributes, 'animation') }}">{{ $content }}</h3>
```

After the view is ready, you can use the shortcode in a WordPress content area.

    [fancy-title animation="wave"]Waving Title[/fancy-title]
    
## Create a Dynamic Shortcode

This can be helpful to create simple shortcodes for objects like Calendars or Employees. It generates a group of shortcodes with a shortcode name related to the object; often slugs work well. For example, calendars with the slug `boise`, `denver`, and `new-york-city` could have shortcode of `[boise-calender]`, `[denver-calender]`, and `[new-york-calender]`.

Create a class implementing the DynamicShortcode interface. A DynamicShortcode requires a shortcodes and render method. The shortcodes method returns an array of Shortcode objects. The render returns a view and it's first argument is a Shortcode object.

```php
<?php 

class CalendarShortcode implements DynamicShortcode
{
    protected $calendars;

    public function __construct(CalendarRepository $calendars)
    {
        $this->calendars = $calendars;
    }

    /**
     * @return Shortcode[]
     */
    public function shortcodes()
    {
        return $this->calendars->all()->map(function ($calendar) {
            return new Shortcode($calendar->id . '-calendar', ['calendarId' => $calendar->id]);
        });
    }

    public function render(Shortcode $shortcode)
    {
        return view('shortcodes.availability-form', [
            'calendarId' => $shortcode->getAttribute('calendarId'),
            'days'       => $this->calendars->getAvailabilityDays(),
            'month'      => Carbon::now(),
        ]);
    }
}
```

Add Dynamic Shortcode class to ShortcodeServiceProvider.php.
```php
class ShortcodeServiceProvider extends BaseShortcodeServiceProvider
{
    protected $dynamicShortcodes = [
        CalendarShortcode::class,
    ];

```

