# Installation

- [Installation](#installation)
    - [Server Requirements](#server-requirements)
    - [Installing LaraPress](#installing-larapress)
- [Configuration](#configuration)
    - [Public Directory](#public-directory)
    - [Configuration Files](#configuration-files)
    - [Directory Permissions](#directory-permissions)
    - [Application Key](#application-key)

<a name="installation"></a>
## Installation

<a name="server-requirements"></a>
### Server Requirements
- PHP >= 5.6.4
- OpenSSL PHP Extension
- PDO PHP Extension
- Mbstring PHP Extension
- Tokenizer PHP Extension
- XML PHP Extension

<a name="installing-larapress"></a>
### Installing LaraPress
LaraPress utilizes [Composer](http://getcomposer.org) to manage its dependencies. So, before using LaraPress, 
make sure you have Composer installed on your machine.

Once installed, you'll run the following command in your terminal:

```
composer create-project lara-press/larapress --prefer-dist
```

<a name="configuration"></a>
### Configuration

#### Public Directory

After installing Laravel, you should configure your web server's document / web root to be the `public` directory. The `index.php` in this directory serves as the front controller for all HTTP requests entering your application.

#### Configuration Files

All of the configuration files for the Laravel framework are stored in the `config` directory. Each option is documented, so feel free to look through the files and get familiar with the options available to you.

#### Directory Permissions

After installing Laravel, you may need to configure some permissions. Directories within the `storage` and the `bootstrap/cache` directories should be writable by your web server or Laravel will not run. If you are using the [Homestead](/docs/{{version}}/homestead) virtual machine, these permissions should already be set.

#### Application Key

The next thing you should do after installing Laravel is set your application key to a random string. If you installed Laravel via Composer or the Laravel installer, this key has already been set for you by the `php artisan key:generate` command.

Typically, this string should be 32 characters long. The key can be set in the `.env` environment file. If you have not renamed the `.env.example` file to `.env`, you should do that now. **If the application key is not set, your user sessions and other encrypted data will not be secure!**
