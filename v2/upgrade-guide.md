# SendPortal v1 to v2 Upgrade Guide

> Please see the "Notable Changes" section at the bottom of this document for a list of changes that could impact your use of SendPortal after the upgrade.

## Requirements

> We recommend creating a database backup for your SendPortal installation before proceeding with the v2 upgrade.

### PHP
SendPortal v2 bumps the minimum supported version of PHP from 7.2.5 to __7.3__.

> We recommend using the latest version of PHP possible, as older versions no longer receive bug fixes or security updates.

### SendPortal
Before upgrading to SendPortal v2, you __must__ make sure you have the latest version of SendPortal v1, __with all migrations run__. If this is not performed, you _will_ encounter issues with the upgrade process.

```bash
cd /path/to/sendportal
composer update
php artisan migrate
```

## Updating To The Latest Version
Get the latest version of SendPortal by performing a git pull from GitHub:

```
cd /path/to/sendportal
git pull origin master
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

## Notable Changes
The following functionality has changed between v1 and v2. Please check to see if any of these changes impact your use of SendPortal before you upgrade.

### API Tokens Are Now On Workspaces
API tokens were previously attached a user, but these have now been moved to a workspace. User API tokens have been removed. To continue using the API you will need to generate an API token for your workspace(s). See [API Introduction](/docs/api/introduction) for more information on how to do this.

### Workspace API Removed
Because API tokens are now per-workspace, the workspace API that allowed a user to fetch a list of workspaces has been removed.

### Segments Renamed To Tags
Segments have been renamed to Tags throughout the application, including the API and database.

### SendPortal As A Package
SendPortal can now be included in an existing application as a package. See [Package Installation](/docs/package-installation) for more details.