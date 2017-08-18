Nginx PHP-FPM
========================
> Sandbox for development - container running Nginx + PHP-FPM

![Docker Pulls](https://img.shields.io/docker/pulls/dockerphp/nginx.svg)
[![Build Status](https://travis-ci.org/php-docker/nginx.svg?branch=master)](https://travis-ci.org/php-docker/nginx)

# Supported tags
| Os      | PHP | Image                       | Layers |
|---------|-----|-----------------------------|--------|
| Wheeze  | 5.6 | dockerphp/nginx:5.6-wheezy  | [![](https://images.microbadger.com/badges/image/dockerphp/nginx:5.6-wheezy.svg)](https://microbadger.com/images/dockerphp/nginx:5.6-wheezy) |
| Jessie  | 5.6 | dockerphp/nginx:5.6-jessie  | [![](https://images.microbadger.com/badges/image/dockerphp/nginx:5.6-jessie.svg)](https://microbadger.com/images/dockerphp/nginx:5.6-jessie) |
| Jessie  | 7.0 | dockerphp/nginx:7.0-jessie  | [![](https://images.microbadger.com/badges/image/dockerphp/nginx:7.0-jessie.svg)](https://microbadger.com/images/dockerphp/nginx:7.0-jessie) |
| Stretch | 7.0 | dockerphp/nginx:7.0-stretch | [![](https://images.microbadger.com/badges/image/dockerphp/nginx:7.0-stretch.svg)](https://microbadger.com/images/dockerphp/nginx:7.0-stretch) |
| Jessie  | 7.1 | dockerphp/nginx:7.1-jessie  | [![](https://images.microbadger.com/badges/image/dockerphp/nginx:7.1-jessie.svg)](https://microbadger.com/images/dockerphp/nginx:7.1-jessie) |
| Stretch | 7.1 | dockerphp/nginx:7.1-stretch | [![](https://images.microbadger.com/badges/image/dockerphp/nginx:7.1-stretch.svg)](https://microbadger.com/images/dockerphp/nginx:7.1-stretch) |

> Based on [Official PHP images Debian](https://hub.docker.com/_/debian/) and all versions come with:

* Dependency Manager:
    * [Composer]
* [Nginx]
* [PHP]
* [Ruby]
* [Sass]
* [Yarn]
* [Git]

# Required

The sandbox uses [Docker][docker], a container tool for setting up a rapid development environment. The project has only two prerequisites:

- [Docker][docker] (1.12+)
- [Docker-composer][docker-compose] (1.10+)

### Basic configuration 

```yaml
version: "2"

services:
    app:
        image: dockerphp/nginx:7.1-jessie
        depends_on:
            - db
            - memcached
        volumes:
            - .:/app
            - /app/var/
        ports:
            - "8080:443"

    db:
        image: mariadb:10.3
        environment:
            MYSQL_ROOT_PASSWORD: root
        ports:
            - "3301:3306"

    memcached:
        image: memcached:latest
        ports:
          - "11221:11211"
        mem_limit: 1g

    pma:
        image: phpmyadmin/phpmyadmin
        depends_on:
            - db
        environment:
            PMA_HOST: db
            PMA_USER: root
            PMA_PASSWORD: root
        ports:
            - "127.0.0.1:8081:80"
```

---

## License

This project is released under the MIT License, you agree to license your code under the [MIT license](LICENSE)

[docker]: https://www.docker.com
[docker-compose]: https://docs.docker.com/compose/install/
[Sass]: http://sass-lang.com/
[Yarn]: https://yarnpkg.com
[Git]: https://git-scm.com/
[PHP]: https://secure.php.net/
[Ruby]: https://www.ruby-lang.org/
[Nginx]: https://nginx.org/
[Composer]: https://getcomposer.org/
