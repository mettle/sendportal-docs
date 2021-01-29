# Package Installation

As of v2, SendPortal officially supports installation as a package in existing Laravel apps, running on Laravel 8 or higher.

## Requirements

- Laravel ≥8
- PHP ≥7.3
- MySQL (≥ 5.7) or PostgreSQL (≥ 9.4)

## Installation

### From Command Line
To install SendPortal as a package from your command line, run the following command:

```bash
composer require mettle/sendportal-core
```

### In `composer.json`
Alternatively, you can add the following to your `composer.json` file:

```json
"mettle/sendportal-core": "^2.0"
```

and then run `composer update` to install it.

## Publish Assets
Run the following command to publish SendPortal's assets:

```bash
php artisan vendor:publish --provider=Sendportal\\Base\\SendportalBaseServiceProvider
```

## Setting Up Resolvers & Routes
SendPortal's functionality is linked to your application through the use of the `Sendportal` facade. The following sections will detail how to use this facade to get SendPortal up and running inside your application.

> Please read all sections and decide their applicability to your use case. Some sections are marked as Required, and will need to be completed for a successful integration with SendPortal. Other sections are marked as Optional and may or may not be required for your own use case.

## Set Up Workspace Resolver (Required)
In order to support multi-tenancy, SendPortal requires whatever is hosting it to provide a "workspace ID" for the session.

The workspace ID will be used in both web and API sessions and will be stored to the database in the `workspace_id` column of tables like `sendportal_campaigns`, `sendportal_subscribers`, etc.

> Multi-tenancy is optional. If your application is not multi-tenant, or you do not wish to use SendPortal in a multi-tenant way, you can provide a hardcoded integer value of your choice to the resolver.

### Registering Workspace Resolver
Inside the `boot` method of a service provider class, provide a closure to the `Sendportal\Base\Facades\Sendportal::setCurrentWorkspaceIdResolver()` method that resolves a workspace ID.

The return value of your closure __must__ be an integer value and __must not__ be null.

As an example:

```php
<?php

declare(strict_types=1);

namespace App\Providers

use Illuminate\Support\ServiceProvider;
use Sendportal\Base\Facades\Sendportal;

class AppServiceProvider extends ServiceProvider
{
    // …

    public function boot(): void
    {
        Sendportal::setCurrentWorkspaceIdResolver(function () {
            return 1;
        });
    }
}
```

## Set Up Sidebar HTML Content Resolver (Optional)
Optionally, you can provide content to the sidebar navigation in SendPortal. This allows you to inject new menu items that can link to resources you build yourself. This is helpful for providing access to things like user management inside SendPortal.

### Registering Sidebar HTML Resolver
Inside the `boot` method of a service provider class, provide a closure to the `Sendportal\Base\Facades\Sendportal::setSidebarHtmlContentResolver()` method.

The return value of your closure __must__ be a string value or null. You should ideally provide HTML, as it will be rendered directly into the view as provided.

As an example:

```php
    public function boot(): void
    {
        Sendportal::setSidebarHtmlContentResolver(function () {
            return view('layouts.sidebar.manageUsersMenuItem')->render();
        });
    }
```

## Set Up Header HTML Content Resolver (Optional)
Optionally, you can provide content to the header in SendPortal. This allows you to inject resources that you build yourself. This is helpful for providing things like user profile management or workspace switchers inside SendPortal.

### Registering Header HTML Resolver
Inside the `boot` method of a service provider class, provide a closure to the `Sendportal\Base\Facades\Sendportal::setHeaderHtmlContentResolver()` method.

The return value of your closure __must__ be a string value or null. You should ideally provide HTML, as it will be rendered directly into the view as provided.

As an example:

```php
    public function boot(): void
    {
        Sendportal::setHeaderHtmlContentResolver(function () {
            return view('layouts.header.userManagementHeader')->render();
        });
    }
```

## Set Up SendPortal Web Routes (Required)
To access SendPortal resources from the browser (e.g. Campaigns, Subscribers, Templates), you must register SendPortal's web routes inside your own application.

### Registering Web Routes
Inside a routes file, call the `Sendportal\Base\Facades\Sendportal::webRoutes()` method. This will register SendPortal's web routes. If called inside a route group, any prefixes, names, middlewares, etc, will be applied.

> These routes include features like subscriber management and campaign sending, and therefore should not be exposed to the internet without some means of authentication.

> SendPortal's route names already include `sendportal.`, so you will not need to provide that yourself. They do not, however, include `sendportal/` in the URL.

As an example:

```php
Route::middleware(['auth'])->prefix('sendportal')->group(function () {
    Sendportal::webRoutes();
});
```

## Set Up SendPortal Public Web Routes (Required)
To provide access to features such as unsubscribing from a mailing list and viewing the email in the browser, you must register SendPortal's public web routes inside your own application.

### Register Public Web Routes
Inside a routes file, call the `Sendportal\Base\Facades\Sendportal::publicWebRoutes()` method. This will register SendPortal's public web routes. If called inside a route group, any prefixes, names, middlewares, etc, will be applied.

> These routes include publically accessible features such as unsubscribing from a mailing list, and therefore should not be guarded by authentication.

As an example:

```php
Sendportal::publicWebRoutes();
```

## Set Up SendPortal API Routes (Optional)
To provide access to API management of SendPortal, you must register SendPortal's API routes inside your own application.

### Register API Routes
Inside a routes file, call the `Sendportal\Base\Facades\Sendportal::apiRoutes()` method. This will register SendPortal's API routes. If called inside a route group, any prefixes, names, middlewares, etc, will be applied.

> These routes include features like subscriber and campaign management, and therefore should not be exposed to the internet without some means of authentication.

As an example:

```php
Route::middleware(['auth:api'])->group(function() {
    Sendportal::apiRoutes();
});
```

## Set Up SendPortal Public API Routes (Required)
To provide access to webhooks for campaign tracking, you must register SendPortal's public API routes inside your own application.

### Register Public API Routes
Inside a routes file, call the `Sendportal\Base\Facades\Sendportal::publicApiRoutes()` method. This will register SendPortal's public web routes. If called inside a route group, any prefixes, names, middlewares, etc, will be applied.

> These routes include webhooks that are needed to track campaigns inside SendPortal, and therefore must be accessible to your email service of choice.

As an example:

```php
Sendportal::publicApiRoutes();
```

## Further Examples
To see an example of SendPortal used as a fully multi-tenant application, please see our own [host application](https://github.com/mettle/sendportal), which takes advantage of all the integration features available in the SendPortal package.

In particular, see the `App\Providers\AppServiceProvider` class for registering resolvers, and see the `routes/web.php` and `routes/api.php` files for registering routes.
