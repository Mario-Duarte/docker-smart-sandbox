# Docker Smart Sandbox

A Docker container meant to create a sandbox environment to run/test small code snippets based on the [Smart Sandbox](https://github.com/Mario-Duarte/Smart-Sandbox) repo that I created and decided to share with everyone.

Hope it helps someone out there!

This container uses:

- php 7.4-apache
- mariadb
- adminer

Feel free to modify and adapt the Dockerfile in `./docker/image/Dockerfile` to your needs but adding and removing extensions and apps.

Currently the Dockerfile will install, `wget git zip unzip openssl zlib1g-dev libcurl3-dev libzip-dev libpng-dev libxml2-dev libmcrypt-dev` as well as `mysqli pdo_mysql json curl gd zip pcntl exif intl` php extensions.

It also creates self-sign certificates that are saved onto `/var/www/conf/` folder to be used by the server, *you may see a warning page when visiting the site with __https__, if so have a look at [this article](https://medium.com/@dblazeski/chrome-bypass-net-err-cert-invalid-for-development-daefae43eb12)  on how to bypass the error on chrome. I would recommend replacing these certificates with ones from [letsencrypt](https://letsencrypt.org/).*

To instal just run `docker-compose build && docker-compose up`.

___

## Database

The default user for the database is `root` and the password is `root`, you can change this in the `./docker-compose.yml` file. 

To connect to the database you can visit `http://localhost:8080/` from your browser to access [adminer](https://www.adminer.org/), or using a software like [sequel pro](https://www.sequelpro.com/) or similar, using the standard port `3306`.

If this port is already in use by another service on you machine you can change this in the `./docker-compose.yml` file.

___

### Other utilities

This container also has `composer`, `NodeJS` latest stable version and `git` so that you can run all of your utilities in the container.

#### Want to help make this container better?
Feel free to get in touch to make suggestions on how I can improve this container to a wider audience, or to report mistakes and issues.
