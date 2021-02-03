# Installation

## Requirements

To run SendPortal, your environment must meet a few minimum requirements:

- PHP ≥ 7.2.5
- Git
- [Composer](https://getcomposer.org/)
- MySQL (≥ 5.7) or PostgreSQL (≥ 9.4)

## Installing SendPortal

### Clone The Repository

Clone the repository to your environment, using the following command:

```bash
git clone https://github.com/mettle/sendportal.git
```

### Install Dependencies

Once cloned, navigate to the project's root directory and run `composer install` to install SendPortal and its dependencies.

From here, you can move onto the [Configuration & Setup](/docs/v1/getting-started/configuration-and-setup) step.

### Webserver

You will need to a webserver (for example, Apache or nginx), in order to host your SendPortal installation.

When setting up your websever, it should be pointed to the `public` directory in order to correctly serve SendPortal.

For example, in nginx:

```
server {
    listen 80;
    server_name campaigns.example.com;
    root /var/www/campaigns.example.com/public;
}
```

For more detailed information, see the [Laravel deployment documentation](https://laravel.com/docs/deployment).
