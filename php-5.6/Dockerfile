FROM php:5.6-fpm

# Create image:
# docker build -t pronego/php:5.6 --build-arg TIMEZONE=Europe/Berlin

ARG TIMEZONE

MAINTAINER Dr. Manuel Lamotte-Schubert <mls@pronego.com>

# copy local files into image
ADD ioncube_loader_lin_5.6.so /usr/local/lib/php/
ADD 00-ioncube.ini /usr/local/etc/php/conf.d/
ADD my-config.ini /usr/local/etc/php/conf.d/

RUN apt-get update && apt-get install -y \
	less \
    openssl \
    git \
    unzip \
	libsodium-dev \
	zlib1g-dev \
	libcurl4-gnutls-dev \
	libpng-dev \
	libfreetype6-dev \
	libjpeg62-turbo-dev \
	sendmail \
    libicu-dev \
    libssh2-1-dev libssh2-1 \
    locales \
    libmcrypt-dev \
	iputils-ping \
	--no-install-recommends \
	&& rm -r /var/lib/apt/lists/* \
	&& printf 'en_US.UTF-8 UTF-8\n' >> /etc/locale.gen \
	&& printf 'de_DE.UTF-8 UTF-8\n' >> /etc/locale.gen \
	&& locale-gen

# Set alias for easier work on console
RUN echo 'alias ll="ls -l --color=auto"' >> ~/.bashrc

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
&& composer --version

# Set timezone
RUN ln -snf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && echo ${TIMEZONE} > /etc/timezone \
&& printf '[PHP]\ndate.timezone = "%s"\n', ${TIMEZONE} > /usr/local/etc/php/conf.d/tzone.ini \
&& "date"

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/

# Type docker-php-ext-install to see available extensions
RUN docker-php-ext-install pdo pdo_mysql mysqli zip mbstring curl iconv gd intl exif mcrypt


# Install xdebug + ssh2
RUN pecl install xdebug-2.5.5 ssh2 \
&& docker-php-ext-enable xdebug ssh2

# Cleanup
RUN apt-get clean && apt-get autoremove -y && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/src

WORKDIR /var/www/app
