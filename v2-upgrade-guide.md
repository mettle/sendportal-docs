# SendPortal v1 To v2 Upgrade Guide

## Requirements

### SendPortal
Before upgrading to SendPortal v2, you __must__ make sure you have the latest version of SendPortal v1, __with all migrations run__. If this isn't done, you _will_ encounter issues with the upgrade process.

> We recommend creating a database backup for your SendPortal installation before proceeding with the v2 upgrade.

### PHP
SendPortal v2 bumps the minimum supported version of PHP from 7.2.5 to __7.3__.

> We recommend using the latest version of PHP possible, as older versions do not receive bug fixes or security updates.

## Getting The Latest Version
Get the latest version of SendPortal by performing a git pull from GitHub:

```
cd sendportal-install-directory
git pull origin master
```

## Applying The Changes
Once the new version is downloaded, you will need to tell SendPortal about the new code. This is done by using the following command:

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

### Manual Upgrade
If you prefer to perform the upgrade steps manually, you will need to do the following:

- Apply migrations with `php artisan migrate`
- Republish assets with `php artisan vendor:publish --provider='Sendportal\Base\SendportalBaseServiceProvider' --force`

## Laravel Horizon
If you are using Laravel Horizon to manage redis queues, you will need to republish its assets for it to continue working with the new version of SendPortal:

```
php artisan horizon:publish
```

> For more information about Horizon, see _Running Redis Queues With Laravel Horizon_ in [Configuration & Setup](/docs/getting-started/configuration-and-setup).

## Complete
If all of these steps complete successfully, you will now have SendPortal v2 installed.
