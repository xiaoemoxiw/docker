######
# See: https://hub.docker.com/_/php/
######

FROM php:7.1.9-fpm
MAINTAINER micooz <micooz@hotmail.com>

######
# You can install php extensions using docker-php-ext-install
######

#RUN cp /etc/apt/sources.list /etc/apt/sources.list.bak

#RUN echo "deb http://mirrors.aliyun.com/debian/ jessie main non-free contrib" > /etc/apt/sources.list \
#    && echo "deb http://mirrors.aliyun.com/debian/ jessie-proposed-updates main non-free contrib" >> /etc/apt/sources.list \
#    && echo "deb-src http://mirrors.aliyun.com/debian/ jessie main non-free contrib" >> /etc/apt/sources.list \
#    && echo "deb-src http://mirrors.aliyun.com/debian/ jessie-proposed-updates main non-free contrib" >> /etc/apt/sources.list

#RUN cat /etc/apt/sources.list.bak >> /etc/apt/sources.list

RUN echo "deb http://mirrors.163.com/debian/ jessie main non-free contrib " > /etc/apt/sources.list \
    && echo "deb http://mirrors.163.com/debian/ jessie-updates main non-free contrib " >> /etc/apt/sources.list \
    && echo "deb http://mirrors.163.com/debian/ jessie-backports main non-free contrib " >> /etc/apt/sources.list \
    && echo "deb-src http://mirrors.163.com/debian/ jessie main non-free contrib " >> /etc/apt/sources.list \
    && echo "deb-src http://mirrors.163.com/debian/ jessie-updates main non-free contrib " >> /etc/apt/sources.list \
    && echo "deb-src http://mirrors.163.com/debian/ jessie-backports main non-free contrib " >> /etc/apt/sources.list \
    && echo "deb http://mirrors.163.com/debian-security/ jessie/updates main non-free contrib " >> /etc/apt/sources.list \
    && echo "deb-src http://mirrors.163.com/debian-security/ jessie/updates main non-free contrib" >> /etc/apt/sources.list


RUN apt-get update
RUN apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        wget \
        git \
        git-gui \
        zip \
        unzip \
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd pdo pdo_mysql zip opcache


#安装composer
WORKDIR /opt
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php --install-dir=/usr/bin --filename=composer
RUN composer config -g repo.packagist composer https://packagist.phpcomposer.com

#安装node
RUN wget https://npm.taobao.org/mirrors/node/v6.11.3/node-v6.11.3-linux-x64.tar.xz \
    && tar xvf node-v6.11.3-linux-x64.tar.xz \
    && mv node-v6.11.3-linux-x64 node \
    && echo export PATH="/opt/node/bin:$PATH" >> /etc/profile \
    && source /etc/profile \
    && npm install -g cnpm --registry=https://registry.npm.taobao.org
#    && ln -s /opt/node/bin/node /usr/bin/ \
#    && ln -s /opt/node/bin/npm /usr/bin/ \
#    && ln -s /opt/node/bin/gulp /usr/bin/ \
#    && alias cnpm="npm --registry=https://registry.npm.taobao.org --cache=$HOME/.npm/.cache/cnpm --disturl=https://npm.taobao.org/dist --userconfig=$HOME/.cnpmrc"




