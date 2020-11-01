FROM php:7.4-fpm-alpine

RUN apk update
# RUN apk add git nano vim sqlite-dev postgresql-dev libxml2-dev curl-dev libcurl gd libmcrypt-dev libjpeg oniguruma-dev freetype-dev php7-dev
RUN apk add git nano vim nodejs npm

RUN npm install -g yarn

RUN yarn add cross-env -g

COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/bin/

# RUN apk add \
#     php7-common\
#     php7-pdo\
#     php7-ctype\
#     php7-pdo\
#     php7-pdo_mysql\
#     php7-pdo_pgsql\
#     php7-pgsql\
#     php7-dom\
#     php7-curl\
#     php7-fileinfo\
#     php7-json\
#     php7-mbstring\
#     php7-openssl\
#     php7-xml\
#     php7-mcrypt\
#     php7-gd\
#     php7-bcmath\
#     php7-imagick

RUN apk add \
    fortune \
    cowsay \
    --update-cache \
    --repository https://alpine.global.ssl.fastly.net/alpine/edge/community \
    --repository https://alpine.global.ssl.fastly.net/alpine/edge/main \
    --repository https://dl-3.alpinelinux.org/alpine/edge/testing
RUN install-php-extensions pdo
RUN install-php-extensions ctype
RUN install-php-extensions pdo_mysql
RUN install-php-extensions pdo_pgsql
RUN install-php-extensions pgsql
RUN install-php-extensions dom
RUN install-php-extensions curl
RUN install-php-extensions fileinfo
RUN install-php-extensions json
RUN install-php-extensions mbstring
RUN install-php-extensions openssl
RUN install-php-extensions xml
RUN install-php-extensions mcrypt
RUN install-php-extensions gd
RUN install-php-extensions bcmath
RUN install-php-extensions imagick


RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === 'c31c1e292ad7be5f49291169c0ac8f683499edddcfd4e42232982d0fd193004208a58ff6f353fde0012d35fdd72bc394') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php --install-dir="/bin" --filename=composer
RUN php -r "unlink('composer-setup.php');"
CMD ["php-fpm", "-F", "-R"]
