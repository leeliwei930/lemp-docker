# LEMP Docker

## Introduction

In this docker-compose configuration which is primary for Laravel PHP Framework Development, and it also can be used for another PHP development such as WordPress

This docker-compose contain a LEMP stack environment.

## Default configuration
By default, the web directory root which is point to `www/public` directory, you can modified it in `nginx/conf/default.conf` configuration file.
If you wish to use other path as web directory you need to update the volume mapping path in `nginx` and `php` services section.

```yaml
volumes: 
        - ./www:/var/www/html/
```

The nginx logs files will be stored in `nginx/logs` folder, once the container get created. In addition, nginx configuration is located in `nginx/conf` directory.

## Environment Variable
The environment variable example is specified in `env-example` file, you need to copy this file as `.env` in order to let docker-compose resolve the variable in the yaml file.

## Usage

### Step 1 : Copy Environment File
```sh
$ cp env-example .env
```

### Step 2: Running the container
```sh
$ docker-compose up -d nginx mariadb php
```

### Step 3: Work in the php container
By default the composer, git and nano command is installed in the php container.
```sh
$ docker-compose exec php sh
```

### Step 4: Run any composer command

``` shell
# /var/www/html: composer  --version
```
## Common Problem
If you saw a message such as ADDR_IN_USE this is commonly caused by the host machine that some of the services that is running and listening to the specific port. Try to stop the services or change the port settings in docker-compose.yaml file.

## More tools
NodeJS, npm and yarn is preinstalled in the php container. So you can run any bundler such as webpack or gulp without any issue, please ensure that those bundler port must be exposed from the container to the host machine by adding the port number in the php services `ports` section `docker-compose.yaml` file.
