# Templates

- [Using Templates](#using-templates)
- [Using Views Within Themes](#using-views-within-themes)

## Using Templates
When you create templates in the `view/templates` folder, they are are available as options in a metabox on post types through WP Admin. 

Also for Posts, Pages, Custom Post Types, template values are available in views with the `$__template` variable. 

Easily switch between templates and custom pages below with this in your master blade file.

```blade
@if (isset($__template))
    @include('templates.' . $__template)
@else
    @yield('content')
@endif
```

## Using Views Within Themes

The standard Laravel way of using the Blade templating is to create your views at `/resources/views/`. This still works
the exact same way. Although if you'd like to keep the views within your theme, LaraPress allows you to create your views
in your theme folder. Just add a `views` folder nested directly under your theme folder and voila, you can now use the same
`view()` Laravel helper function to return views.

*Note: the views nested in your theme folder will override any views located in the resources folder.*