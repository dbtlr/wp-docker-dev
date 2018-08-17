# WordPress Docker Development Enviorment

## Quick Start

This assumes you have [Composer](https://getcomposer.org) installed locally to help orchastrate local tools.

```bash
composer create-project dbtlr/wp-docker-dev wp-site
```

This will create a new `wp-site` directory, download the dependencies, and will also ask you a series of questions that are used to build a `.env` file which will be used to configure your Docker deploy.

Here's an example of the .env file that is created:

```
NAME=wp
DOMAIN=wp.loc
PHP_VERSION=7.2
WORDPRESS_VERSION=latest
MYSQL_ROOT_PASSWORD=rootpassword
IP_ROOT=172.16.200
```

Yous should also add an entry to your `/etc/hosts` file that maps the DOMAIN above to 127.0.0.1

If you're running multiple Docker instances, then change the IP_ROOT to another number, i.e. `172.16.201` to avoid conflicts.

### Launch Docker Compose

```bash
docker-compose up
```

Once you see `Command line: 'apache2 -D FOREGROUND'` has completed, you should be able to navigate to http://$DOMAIN in your web browser.

If you wish to run Docker in the background, use

```bash
docker-compose up -d
```

In order to halt a Docker container running in the background, instead use:

```bash
docker-compose down
```

## Your files

In the `src/` directory you'll find 3 folders:

- `src/mu-plugins`
- `src/plugins`
- `src/themes`

These are read-only mounts that you're able to update, but that the Docker container cannot change. This is done by default so that you handle maintaining your files using source control and not allow WordPress to accidently destory your work through its own automated install process.

Consider managing your plugins and themes using [WPackagist](https://wpackagist.org/) instead. For your convenience, the basic composer configuration is included.

