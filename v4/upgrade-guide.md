# SendPortal v3 to v4 Upgrade Guide

SendPortal v4 upgrades SendPortal to Laravel 13. Laravel 11, which SendPortal v3 is built on, no longer receives security fixes, and recent versions of Composer will refuse to install or update SendPortal v3's dependencies because of known security advisories. We recommend upgrading to v4 as soon as possible.

> Please see the "Notable Changes" section at the bottom of this document for a list of changes that could impact your use of SendPortal after the upgrade.

> If you do not wish to upgrade to v4, please see the "Remaining On v3" section at the bottom of this document.

## Requirements

> We recommend creating a database backup for your SendPortal installation before proceeding with the v4 upgrade.

### PHP
SendPortal v4 bumps the minimum supported version of PHP from 8.2 to __8.3__.

> We recommend using the latest version of PHP possible, as older versions no longer receive bug fixes or security updates.

### Laravel
The stand-alone SendPortal application now runs on Laravel 13.

If you use SendPortal as a package, your application must be running Laravel 12 or 13 before you upgrade. See the [Laravel upgrade guide](https://laravel.com/docs/13.x/upgrade) for details on upgrading your application.

### Database
SendPortal v4 requires PostgreSQL 10 or later, up from 9.4. The minimum MySQL version is unchanged at 5.7.

## Updating To The Latest Version
To get the latest version of SendPortal, you must checkout the new v4 tag.

First, ensure you are in your SendPortal installation directory:

```
cd /path/to/sendportal
```

Then use git to fetch and checkout the `v4.0.0` tag:

```
git fetch --tags
git checkout v4.0.0
```

> If you have made your own changes to SendPortal's files, git may not be able to checkout the new tag until you commit or stash those changes, and you may need to resolve conflicts with the changes made for Laravel 13.

Finally, update SendPortal's dependencies:

```
composer update
```

## Performing The Upgrade
Once you have the new version of SendPortal on your system, you will need to perform an upgrade to ensure your installation works correctly.

### Automatic Upgrade
SendPortal includes an upgrade command that performs the necessary upgrade steps for you, similar to the initial setup command. To use it, run the following:

```
php artisan sp:upgrade
```

> When the command finishes, it reports that SendPortal has been upgraded to "version 2". This message has not been updated for v4, and can be safely ignored.

### Manual Upgrade
If you prefer to perform the upgrade steps manually, you will need to do the following:

Apply migrations:
```
php artisan migrate
```

Republish assets:
```
php artisan vendor:publish --provider='Sendportal\Base\SendportalBaseServiceProvider' --force
```

> SendPortal v4 does not add any database migrations, but running `migrate` will apply any migrations from v3 that you have not yet run.

## Laravel Horizon
Laravel Horizon no longer publishes its assets, so you no longer need to run `php artisan horizon:publish` after upgrading. If your deployment scripts still run it, you can remove it; it only prints a warning.

## Upgrading SendPortal As A Package
If you use SendPortal as a package inside your own application, first make sure your application is running Laravel 12 or 13 and PHP 8.3 or later.

Then update the SendPortal requirement in your `composer.json` file:

```json
"mettle/sendportal-core": "^4.0"
```

Run `composer update` to install it, then apply migrations and republish SendPortal's assets:

```
php artisan migrate
php artisan vendor:publish --provider='Sendportal\Base\SendportalBaseServiceProvider' --force
```

## Notable Changes
The following functionality has changed between v3 and v4. Please check to see if any of these changes impact your use of SendPortal before you upgrade.

### CSRF Middleware Renamed
Laravel 13 renamed its CSRF protection middleware from `VerifyCsrfToken` to `PreventRequestForgery`. The stand-alone application's `App\Http\Middleware\VerifyCsrfToken` class has been renamed to `App\Http\Middleware\PreventRequestForgery` to match.

If you added any URIs to the `$except` list of the old middleware, move them to the new `app/Http/Middleware/PreventRequestForgery.php` file.

The new middleware also accepts form submissions that the browser marks as coming from the same origin, in addition to checking the CSRF token.

### Laravel 13
The stand-alone application has been upgraded from Laravel 11 to Laravel 13. If you have added your own code to the stand-alone application, see the Laravel [12](https://laravel.com/docs/12.x/upgrade) and [13](https://laravel.com/docs/13.x/upgrade) upgrade guides for changes that may affect it.

## Remaining On v3
If you are not yet ready to upgrade to v4, you will need to ensure you are using a v3 tag.

> Laravel 11 stopped receiving security fixes in March 2026. Remaining on v3 leaves your installation exposed to known vulnerabilities, and Composer will refuse to install or update its dependencies unless you disable its security checks.

To check whether you are using a tagged version, navigate to your SendPortal installation and run the following command:

```
git status
```

If you see `HEAD detached at v3.0.1`, or another number starting `v3`, then you are using a tagged version and don't need to do anything else.

If you see `On branch master`, then you will need to switch to a tagged version in order to avoid any risk of getting unwanted changes.

To do this, run the following command:

```
git checkout v3.0.1
```

If you run the `git status` command again you should now see the correct message. You will now be able to continue running v3 of SendPortal without getting unwanted changes. If you want to then go on to perform an upgrade to v4 at a later date, come back to this document and follow the upgrade instructions.

If you use SendPortal as a package, keep your `composer.json` requirement at `"mettle/sendportal-core": "^3.0"`.
