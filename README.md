# Docker PHP Development Environment

Alpha/ Targeted at Windows (git-bash/mingw) for the moment.

* Ubuntu 16.04
* Nginx
* PHP 7.2-fpm
* Intl Extension
* Imagemagick
* XDebug
* Supervisor
* MySQL 5.7
* Redis 4.0.9

## Usage

Use the `./develop` script for a less verbose way of working with the containers

There are shortcuts for `exec`, `php`, `composer`, `npm` and `gulp`. Other commands get passed through to `docker-compose`.

```bash
./develop up --build
./develop down
./develop run app bash -it
./develop php -v
./develop composer require vendor/package
./develop npm install
./develop gulp
```

## Thanks

 * [Shipping Docker](https://serversforhackers.com/shipping-docker)