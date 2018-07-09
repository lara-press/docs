# Plugins

- [Tribe Events Calendar](#tribe-events-calendar)
- [Plugin Custom Post Type Routing](/routing.md#use-custom-types-from-a-plugin)

##Tribe Events Calendar

Controller

```php
<?php

use Illuminate\Http\Request;

class EventsController extends Controller
{
    public function handle(Request $request)
    {
        if ($request->get('ical')) {

            $iCal = new \Tribe__Events__iCal;

            $iCal->generate_ical_feed(get_post(post()->ID));
        }

        if (is_single()) {
            return view('events');
        }

        return view('events');
    }
```

Use the following view, then you can [customize](https://theeventscalendar.com/knowledgebase/themers-guide/) the templates as needed.

```blade
    <div id="tribe-events-pg-template">
        @php(tribe_events_before_html())
        @php(tribe_get_view())
        @php(tribe_events_after_html())
    </div> <!-- #tribe-events-pg-template -->
```