FROM php:7.3.33-fpm-alpine

# 更换国内源
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories

# 安装依赖软件
RUN apk add --no-cache libpng-dev libzip-dev icu-dev

# 安装PHP扩展
RUN mkdir -p /usr/src/php/ext
RUN docker-php-source extract

RUN curl -o redis-5.3.5.tgz http://pecl.php.net/get/redis-5.3.5.tgz \
	&& tar -zxf redis-5.3.5.tgz \
	&& rm -f redis-5.3.5.tgz \
	&& mv redis-5.3.5 /usr/src/php/ext/redis \
	&& rm -f package.xml

RUN curl -o xdebug-3.1.3.tgz http://xdebug.org/files/xdebug-3.1.3.tgz \
	&& tar -zxf xdebug-3.1.3.tgz \
        && rm -f xdebug-3.1.3.tgz \
        && mv xdebug-3.1.3 /usr/src/php/ext/xdebug \
        && rm -f package.xml

RUN docker-php-ext-install gd \
	&& docker-php-ext-install bcmath \
	&& docker-php-ext-install zip \
	&& docker-php-ext-install pdo_mysql \
	&& docker-php-ext-install intl \
	&& docker-php-ext-install redis \
    && docker-php-ext-install xdebug

# 安装composer包管理
RUN curl -o composer.phar https://install.phpcomposer.com/composer.phar \
	&& mv composer.phar /usr/local/bin/composer \
	&& chmod +x /usr/local/bin/composer

EXPOSE 9000 9003 9002
