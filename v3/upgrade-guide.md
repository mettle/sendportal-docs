# SendPortal v2 to v3 Upgrade Guide

> Please see the "Notable Changes" section at the bottom of this document for a list of changes that could impact your use of SendPortal after the upgrade.

> If you do not wish to upgrade to v3, please see the "Remaining On v2" section at the bottom of this document.

## Requirements

> We recommend creating a database backup for your SendPortal installation before proceeding with the v3 upgrade.

### PHP
SendPortal v3 bumps the minimum supported version of PHP from 7.3 to __8.2__.

> We recommend using the latest version of PHP possible, as older versions no longer receive bug fixes or security updates.

### Laravel
The stand-alone SendPortal application now runs on Laravel 11.

If you use SendPortal as a package, your application must be running Laravel 10 or 11 before you upgrade. See the [Laravel upgrade guide](https://laravel.com/docs/11.x/upgrade) for details on upgrading your application.

## Updating To The Latest Version
To get the latest version of SendPortal, you must checkout the new v3 tag.

First, ensure you are in your SendPortal installation directory:

```
cd /path/to/sendportal
```

Then use git to fetch and checkout the `v3.0.1` tag:

```
git fetch --tags
git checkout v3.0.1
```

> If you have made your own changes to SendPortal's files, git may not be able to checkout the new tag until you commit or stash those changes, and you may need to resolve conflicts with the changes made for Laravel 11.

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

> When the command finishes, it reports that SendPortal has been upgraded to "version 2". This message has not been updated for v3, and can be safely ignored.

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

## Laravel Horizon
If you are using Laravel Horizon to manage redis queues, you will need to republish its assets for it to continue working with the new version of SendPortal:

```
php artisan horizon:publish
```

> Laravel Horizon stopped publishing its assets in version 5.24.4. If you have Horizon 5.24.4 or later installed (`composer show laravel/horizon`), this command only prints a warning and can be skipped.

> For more information about Horizon, see _Running Redis Queues With Laravel Horizon_ in [Configuration & Setup](/docs/v3/getting-started/configuration-and-setup).

## Upgrading SendPortal As A Package
If you use SendPortal as a package inside your own application, first make sure your application is running Laravel 10 or 11 and PHP 8.2 or later.

Then update the SendPortal requirement in your `composer.json` file:

```json
"mettle/sendportal-core": "^3.0"
```

Run `composer update` to install it, then apply migrations and republish SendPortal's assets:

```
php artisan migrate
php artisan vendor:publish --provider='Sendportal\Base\SendportalBaseServiceProvider' --force
```

## Notable Changes
The following functionality has changed between v2 and v3. Some of these changes were first released in later v2 versions, so you may already have them. Please check to see if any of these changes impact your use of SendPortal before you upgrade.

### Mailgun Webhook Key
SendPortal now verifies Mailgun webhooks using your Mailgun HTTP webhook signing key, instead of your API key. If you use Mailgun, you will need to edit each Mailgun email service in SendPortal and fill in the new `Webhook Key` field. Until you do, Mailgun webhooks will be rejected and no tracking data will be recorded. See [Mailgun](/docs/v3/email-services/mailgun) for more information.

### Postal Email Service
SendPortal can now send email through [Postal](/docs/v3/email-services/postal), an open-source mail server that you host yourself.

### Laravel 11 And Livewire 3
The stand-alone application has been upgraded to Laravel 11 and Livewire 3. If you have added your own code to the stand-alone application, you may need to update it for these versions.

## Remaining On v2
If you are not yet ready to upgrade to v3, you will need to ensure you are using a v2 tag.

To check whether you are using a tagged version, navigate to your SendPortal installation and run the following command:

```
git status
```

If you see `HEAD detached at v2.0.4`, or another number starting `v2`, then you are using a tagged version and don't need to do anything else.

If you see `On branch master`, then you will need to switch to a tagged version in order to avoid any risk of getting unwanted changes.

To do this, run the following command:

```
git checkout v2.0.4
```

If you run the `git status` command again you should now see the correct message. You will now be able to continue running v2 of SendPortal without getting unwanted changes. If you want to then go on to perform an upgrade to v3 at a later date, come back to this document and follow the upgrade instructions.

If you use SendPortal as a package, keep your `composer.json` requirement at `"mettle/sendportal-core": "^2.0"`.
