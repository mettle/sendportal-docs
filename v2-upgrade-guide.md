# SendPortal v1 To v2 Upgrade Guide

## Requirements
Before upgrading to SendPortal v2, you must make sure you have completed all possible upgrades of SendPortal v1. If this isn't done, you may encounter issues with the upgrade process.

## Upgrading

### Getting The Latest Version
Get the latest version of SendPortal by performing a git pull from GitHub:

```
# cd sendportal-install-directory
# git pull
```

### Applying The Changes
Once the new version is downloaded, you will need to apply the new changes, which you can do with a Composer update:

```
composer update
```

### Apply Migrations
The new version of SendPortal prefixes its core database tables with `sendportal_`. To ensure that SendPortal continues to work, you will need to run migrations so this change can be made to your existing database:

```
php artisan migrate
```

### Republish Assets
SendPortal v2 makes changes to various views, routes, etc. To ensure these are available, you need to republish SendPortal's assets:

```
php artisan vendor:publish --provider='Sendportal\Base\SendportalBaseServiceProvider' --force
```

### Laravel Horizon
If you are using Laravel Horizon to manage redis queues, you will need to republish its assets for it to continue working with the new version of SendPortal:

```
php artisan horizon:publish
```

> For more information about Horizon, see _Running Redis Queues With Laravel Horizon_ in [Configuration & Setup](/docs/getting-started/configuration-and-setup).
