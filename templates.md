# Templates

- [Using Templates](#using-templates)

## Using Templates

On Posts, Pages, and Custom Post Types, designate available templates with the `getAvailableTemplates` function. Post template values are available in views with the `$__template` variable.

```blade
class Project extends Post implements CustomPostType
{
    public function getAvailableTemplates() {
        return ['one-column', 'two-column'];
    }
```

Easily switch between templates and custom pages below with this in your blade file. Just add blade files named after your available templates in the `resources/template` folder. (i.e.: `one-column.blade.php` and `two-column.blade.php`)

```blade
@if (isset($__template))
    @include('template.' . $__template)
@else
    @yield('content')
@endif
```
