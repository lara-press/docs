# Installation

  - [Installing LaraPress](#installing-larapress)

## Installing LaraPress
 
The framework installs onto the [Larvel](https://laravel.com/docs/7.x/installation) Framework. Requirements are found in the Laravel [docs](https://laravel.com/docs/7.x/installation).

### Via LaraPress Installer
Install with the [Installer](https://github.com/lara-press/installer).

1. Add this repository to the global composer.json. (Since the install is a fork, it's not on packagist).

```
"repositories": [
    {   
        "url": "https://github.com/lara-press/installer.git",
        "type": "git"
    }   
]
```

2. Then run `composer global require lara-press/installer`.

3. After that, create a new LaraPress project with `larapress new blog`

### Manually

1. Setup a [Laravel](https://laravel.com/docs/7.x/installation) project.

2. Setup a database.

3. Add database credentials to the .env.

4. Merge the following to the composer.json.

```
    "require": {
        "funkjedi/composer-include-files": "^1.0",
        "johnpbloch/wordpress": "~5.4",
        "lara-press/framework": "~7.0",
    },
    "extra": {
        "include_files": [
            "public/cms/wp-includes/pomo/translations.php",
            "public/cms/wp-includes/l10n.php"
        ],
        "installer-paths": {
            "public/content/mu-plugins/{$name}/": [
                "larapress/framework"
            ]   
        },  
        "wordpress-install-dir": "public/cms"
    },  
```

5. Run composer install.

6. Run this artisan command to publish all LaraPress files. 

`php artisan vendor:publish --provider="LaraPress\Foundation\Providers\PublishServiceProvider" --force`

