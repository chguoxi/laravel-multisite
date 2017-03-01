# Multiple sites on one codebase

[![Latest Version on Packagist](https://img.shields.io/packagist/v/appstract/laravel-multisite.svg?style=flat-square)](https://packagist.org/packages/appstract/laravel-multisite)
[![Total Downloads](https://img.shields.io/packagist/dt/appstract/laravel-multisite.svg?style=flat-square)](https://packagist.org/packages/appstract/laravel-multisite)
[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE.md)
[![Build Status](https://img.shields.io/travis/appstract/laravel-multisite/master.svg?style=flat-square)](https://travis-ci.org/appstract/laravel-multisite)

With this package it is possible to build multiple sites/(sub)domains on one codebase.

## Installation

You can install the package via composer:

``` bash
composer require appstract/laravel-multisite
```

## Usage

### Config (hosts, homestead)

First of all, you need to add the sites to your `/etc/hosts` file and `Homestead.yaml`. For example, `mywebsite.dev` and `blog.mywebsite.dev`. In the `Homestead.yaml, you need to map the sites to the same folder.

### Publish

Within you Laravel project, run `php artisan vendor:publish --provider="Appstract\Multisite\MultisiteServiceProvider"` to publish all files used by laravel-multisite. The files that will be published are: a migration, a seeder and a config file.

### Seeder

The seeder will be published but needs to be run when running `php artisan db:seed`, so you need the add `$this->call(SitesTableSeeder::class);` to your `DatabaseSeeder.php` file. The sites are now present in the database.

### Routes

This is the main part, within your `routes/web.php` you can set routes for your sites within route groups, like this:

```
Route::group([
    'domain' => 'blog.'.config('multisite.host'),
    'as' => 'blog.',
    'middleware' => 'site:blog'
], function () {

    Route::get('/', 'BlogController@homepage')->name('homepage');

});
```

## Testing

``` bash
$ composer test
```

## Contributing

Contributions are welcome, [thanks to y'all](https://github.com/appstract/laravel-multisite/graphs/contributors) :)

## About Appstract

Appstract is a small team from The Netherlands. <3 Laravel, Vue and other awesome tools.

## Buy Us A Beer

Would be awesome if you would [buy us a beer](https://www.paypal.me/teamappstract/10)! Or [a lot of beer](https://www.patreon.com/appstract) :)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
