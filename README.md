# LEMP Docker

## Introduction

In this docker-compose configuration which is primary for Laravel PHP Framework Development, and it also can be used for another PHP development such as WordPress

This docker-compose contain a LEMP stack environment.

## Default configuration
By default, the web directory root which is point to the parent directory, you can modified it in `docker-compose.yaml` nginx services volumes section.

```yaml
volumes: 
        - ../:/var/www/html/
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
$ docker-compose up -d
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

