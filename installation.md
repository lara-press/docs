#Installation

- [Installation](#installation)
    - [Server Requirements](#server-requirements)
    - [Installing LaraPress](#installing-larapress)
- [Configuration](#configuration)
    - [Basic Configuration](#basic-configuration)
    - [Directory Permissions](#directory-permissions)
    - [Application Key](#application-key)
- [Maintenance Mode](#maintenance-mode)
    - [Maintenance Mode Template](#maintenance-mode-template)
    - [Maintenance Mode & Queues](#maintenance-mode-queues)

<a name="installation"></a>
##Installation

<a name="server-requirements"></a>
###Server Requirements
- PHP >= 5.5.9
- OpenSSL PHP Extension
- PDO PHP Extension
- Mbstring PHP Extension
- Tokenizer PHP Extension

<a name="installing-larapress"></a>
###Installing LaraPress
LaraPress utilizes [Composer](http://getcomposer.org) to manage its dependencies. So, before using LaraPress, 
make sure you have Composer installed on your machine.

Once installed, you'll run the following command in your terminal:

```
composer create-project lara-press/larapress --prefer-dist
```

<a name="configuration"></a>
##Configuration

<a name="basic-configuration"></a>
###Basic Configuration
All of the configuration files for the LaraPress framework are stored in the config directory.

<a name="directory-permissions"></a>
###Directory Permissions
After installing LaraPress, you may need to configure some permissions. Directories within the `storage` and the 
`bootstrap/cache` directories should be writable by your web server. 

<a name="application-key"></a>
###Application Key
The next thing you should do after installing LaraPress is set your application key to a random string. 
If you installed LaraPress via Composer, this key has already been set for you by the `key:generate` command. 
Typically, this string should be 32 characters long. The key can be set in the `.env` environment file. 
If you have not renamed the `.env.example` file to `.env`, you should do that now.  

**If the application key is not set, your user sessions and other encrypted data will not be secure!**

<a name="maintenance-mode"></a>
##Maintenance Mode
When your application is in maintenance mode, a custom view will be displayed for all requests into your application. 
This makes it easy to "disable" your application while it is updating or when you are performing maintenance. 
A maintenance mode check is included in the default middleware stack for your application. If the application is in 
maintenance mode, an `HttpException` will be thrown with a status code of 503.

To enable maintenance mode, simply execute the `down` Artisan command:  

```php artisan down```

To disable maintenance mode, use the `up` command:  

```php artisan up```

<a name="maintenance-mode-template"></a>
###Maintenance Mode Response Template
The default template for maintenance mode responses is located in `resources/views/errors/503.blade.php`.

<a name="maintenance-mode-queues"></a>
###Maintenance Mode & Queues
While your application is in maintenance mode, no queued jobs will be handled. The jobs will continue to be 
handled as normal once the application is out of maintenance mode.