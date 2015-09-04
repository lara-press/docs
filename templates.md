#Templates

- [Using Views Within Themes](#using-views-within-themes)

<a name="using-views-within-themes"></a>
##Using Views Within Themes

The standard Laravel way of using the Blade templating is to create your views at `/resources/views/`. This still works
the exact same way, although if you'd like to keep the views within your theme, LaraPress allows you to create your views
in your theme folder. Just add a `views` folder nested directly under your theme folder and voila, you can now use the same
`view()` Laravel helper function to return views.

*Note: the views nested in your theme folder will override any views located in the resources folder.*