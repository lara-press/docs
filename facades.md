# Facades

#### Action: LaraPress/Actions/Dispatcher.php
```php
Action::listen('init', function() {
    //
});
```

#### Filter: LaraPress/Filters/Dispatcher.php
```php
Filter::listen('init', function() {
    //
});
```

#### PostType: LaraPress/Posts/PostTypeManager.php
```php
PostType::all()
```

#### Loop: LaraPress/Posts/Loop.php

#### Query: LaraPress/Posts/Query.php How is this used?

#### Taxonomy: LaraPress/Posts/TaxonomyManager.php
```php
Taxonomy::all()
```

#### Asset: LaraPress/Assets/Manager
```php
Asset::enqueueScript('test', 'test');
```