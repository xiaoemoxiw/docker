######
# See: https://hub.docker.com/_/php/
######

FROM php:7.1.9-fpm
MAINTAINER micooz <micooz@hotmail.com>

######
# You can install php extensions using docker-php-ext-install
######

RUN sudo echo "deb http://mirrors.aliyun.com/debian/ jessie main non-free contrib \
    deb http://mirrors.aliyun.com/debian/ jessie-proposed-updates main non-free contrib \
    deb-src http://mirrors.aliyun.com/debian/ jessie main non-free contrib \
    deb-src http://mirrors.aliyun.com/debian/ jessie-proposed-updates main non-free contrib" \
    >> /etc/apt/sources.list

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd pdo pdo_mysql \
    && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    && php composer-setup.php --install-dir=/usr/bin

