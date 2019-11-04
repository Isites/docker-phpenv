FROM php:7.2-fpm

RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
&& docker-php-ext-install -j$(nproc) iconv \
&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
&& docker-php-ext-install -j$(nproc) gd

# 增加pdo mysql
RUN docker-php-ext-install -j$(nproc) pdo_mysql mysqli sockets exif

# 增加 soap wddx xmlrpc tidy xsl 扩展
RUN apt-get install -y --no-install-recommends libxml2-dev libtidy-dev libxslt1-dev && \
    rm -r /var/lib/apt/lists/* && \
docker-php-ext-install -j$(nproc) soap wddx xmlrpc tidy xsl

#zip 扩展
RUN apt-get install -y --no-install-recommends zlib1g-dev && \
    rm -r /var/lib/apt/lists/* && \
#docker-php-ext-configure zip --with-libzip && \
docker-php-ext-install -j$(nproc) zip
# mcrypt 扩展 
# RUN apt-get install -y --no-install-recommends libmcrypt && \
# rm -r /var/lib/apt/lists/* && \
# pecl install mcrypt-1.0.1 && \
# docker-php-ext-enable mcrypt

# 增加 Memcached 扩展 
RUN apt-get update && apt-get install -y --no-install-recommends zlib1g-dev libmemcached-dev && \
rm -r /var/lib/apt/lists/* && \
pecl install memcached && \
docker-php-ext-enable memcached

# 增加 opcache 扩展 
RUN docker-php-ext-configure opcache --enable-opcache && docker-php-ext-install opcache

# 增加redis 扩展
RUN pecl install redis-4.0.1 && docker-php-ext-enable redis

# 增加 imagick 扩展
RUN export CFLAGS="$PHP_CFLAGS" CPPFLAGS="$PHP_CPPFLAGS" LDFLAGS="$PHP_LDFLAGS" && \
apt-get update && apt-get install -y --no-install-recommends libmagickwand-dev && \
rm -rf /var/lib/apt/lists/* && \
pecl install imagick-3.4.3 && \
docker-php-ext-enable imagick