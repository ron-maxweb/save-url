# Laravel 5: Save-URL

## Introduction

This package allows you to easily redirect users to the last visited page on login.

## Laravel compatibility

 Laravel  | translation
:---------|:----------
 5.1.x    | 1.0.x
 5.2.x    | 1.0.1 and up
 5.3.x    | 1.0.2 and up
 5.4.x    | 1.0.3 and up

## Installation

Require through composer

	composer require maxweb/save-url 1.0.x

Or manually edit your composer.json file:

	"require": {
		"maxweb/save-url": "1.0.x"
	}

Publish the configuration file:

	php artisan vendor:publish --provider="Waavi\SaveUrl\SaveUrlServiceProvider"

## Usage

### Cached urls
By default, the last visited URL visited by a user is saved in Session. URLs must follow these criteria to be saved:

	- Only GET requests are saved.
	- AJAX requests are not saved.
	- If the user is logged in, no urls are saved.

### Excluding urls from the cache
If you want to exclude certain urls from the url cache, like for example the login and signup pages, you may use the provided "doNotSave" middleware:

```php
// routes/web.php

Route::get('/login', ['middleware' => 'doNotSave', 'uses' => 'AuthController@login']);
```

### Redirecting after login
To redirect the user to the last saved url, such as after authentication, you may use:

```php
public function login() {
	/** Auth user **/
	if ($success) {
		redirect()->toSavedUrl();
	}
}
```
