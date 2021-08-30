# docker-php-nginx-redis-postgres

PHP 7.4
POSGRE 12

This is a backend stack of decoupled technologies in docker containers.
If you have installed docker-compose only use

```bash
docker-compose up --build
```
it uses a HA proxy, which is for ease of use of multiple domains and scaling of containers based on domains.

first you need to define the domain name on

```bash
vi /etc/hosts
```
add to the line of the file

```bash
127.0.0.1 local.test
```

this docker file supports laravel environment

Otherwise please follow the steps in the [official docker documentation](https://docs.docker.com/install/linux/docker-ce/debian/) to install docker compose

## Thanks :)
