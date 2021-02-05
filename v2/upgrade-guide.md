# SendPortal v1 to v2 Upgrade Guide

> Please see the "Notable Changes" section at the bottom of this document for a list of changes that could impact your use of SendPortal after the upgrade.

> If you do not wish to upgrade to v2, please see the "Sticking With v1" section at the bottom of this document.

## Requirements

> We recommend creating a database backup for your SendPortal installation before proceeding with the v2 upgrade.

### PHP
SendPortal v2 bumps the minimum supported version of PHP from 7.2.5 to __7.3__.

> We recommend using the latest version of PHP possible, as older versions no longer receive bug fixes or security updates.

## Updating To The Latest Version
To get the latest version of SendPortal, you must checkout the new v2 tag.

First, ensure you are in your SendPortal installation directory:

```
cd /path/to/sendportal
```

Then use git to checkout the `v2.0.0` tag:

```
git checkout v2.0.0
```

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

> For more information about Horizon, see _Running Redis Queues With Laravel Horizon_ in [Configuration & Setup](/docs/v2/getting-started/configuration-and-setup).

## Notable Changes
The following functionality has changed between v1 and v2. Please check to see if any of these changes impact your use of SendPortal before you upgrade.

### API Tokens Are Now On Workspaces
API tokens were previously attached to a user, but these have now been moved to a workspace. User API tokens have been removed. To continue using the API you will need to generate an API token for your workspace(s). See [API Introduction](/docs/v2/api/introduction) for more information on how to do this.

### Workspace API Removed
Because API tokens are now per-workspace, the workspace API that allowed a user to fetch a list of workspaces has been removed.

### Segments Renamed To Tags
Segments have been renamed to Tags throughout the application, including the API and database.

### SendPortal As A Package
SendPortal can now be included in an existing application as a package. See [Package Installation](/docs/v2/getting-started/package-installation) for more details.

## Sticking With v1
If you are not yet ready to upgrade to v2, you will need to ensure you are using a v1 tag. You may already be doing this; however, previous versions of SendPortal were installed by tracking the "master" branch, which always includes the very latest changes.

To check whether you are using a tagged version, navigate to your SendPortal installation and run the following command:

```
git status
```

If you see `HEAD detached at v1.0.3`, then you are using a tagged version and don't need to do anything else.

If you see `On branch master`, then you will need to switch to a tagged version in order to avoid any risk of getting unwanted changes.

To do this, run the following command:

```
git checkout v1.0.3
```

If you run the `git status` command again you should now see the correct message. You will now be able to continue running v1 of SendPortal without getting unwanted changes. If you want to then go on to perform an upgrade to v2 at a later date, come back to this document and follow the upgrade instructions.

> If you haven't updated your SendPortal installation for some time, v1.0.3 may include changes you haven't previously applied. You should consider running `composer update` followed by `php artisan migrate` to apply any fixes and features included in v1 you may not already have.
