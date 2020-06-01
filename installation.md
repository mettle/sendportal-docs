# Installation

## Requirements

To run SendPortal, your environment must meet a few minimum requirements:

- PHP ≥ 7.2.5
- Git
- [Composer](https://getcomposer.org/)
- MySQL or PostgreSQL

## Installing SendPortal

There are two options for installing SendPortal:

1. Use the official SendPortal project, which is pre-configured with everything you need to get up and running. **(Recommended)**
2. Install SendPortal as a Composer package in an existing project.

### Using The Official SendPortal Project (Recommended)

The official pre-configured SendPortal project includes everything you need to get up and running in the quickest possible time.

#### Clone The Repository

Clone the repository to your environment, using the following command:

```bash
git clone https://github.com/sendportal/sendportal.git
```

#### Install Dependencies

Once cloned, navigate to the project's root directory and run `composer install` to install SendPortal and its dependencies.

From here, you can move onto the [Configuration & Setup](/docs/getting-started/configuration-and-setup) step.

### With Your Own Host Project

This part of the documentation assumes that you are familiar with [Laravel](https://laravel.com). If you are not familiar with Laravel and are unsure where to begin, you may wish to familiarise yourself with the [official framework documentation](https://laravel.com/docs/) before continuing.

#### Install The Package

Install the SendPortal Base package via composer:

```bash
composer require sendportal/sendportal
```

#### Environment Configuration

Now that the package is installed, it's time to configure your environment. Edit the `.env` file and make sure that your database connection and mail driver are set correctly, as specified in the Configuration & Setup section.

#### Update The User Provider

Next, you must navigate to your `config/auth.php` file and change the default `providers.users.model` value to `\Sendportal\Base\Models\User::class`. This will allow the SendPortal package to manage user authentication.

SendPortal should now be successfully installed. You can now follow the [Configuration & Setup](/docs/getting-started/configuration-and-setup) process.
