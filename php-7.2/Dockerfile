FROM php:7.2-fpm

# Create image:
# docker build -t pronego/php:7.2 --build-arg TIMEZONE=Europe/Berlin

ARG TIMEZONE

MAINTAINER Dr. Manuel Lamotte-Schubert <mls@pronego.com>

# copy local files into image
ADD ioncube_loader_lin_7.2.so /usr/local/lib/php/
ADD 00-ioncube.ini /usr/local/etc/php/conf.d/
ADD my-config.ini /usr/local/etc/php/conf.d/

RUN apt-get update && \
    apt-get install -y libxml2-dev \
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
    libssh2-1-dev \
    libxml2-dev \
    locales \
    libmcrypt-dev \
    gnupg \
    iputils-ping \
	--no-install-recommends \
	&& rm -r /var/lib/apt/lists/* \
	&& printf 'en_US.UTF-8 UTF-8\n' >> /etc/locale.gen \
	&& printf 'de_DE.UTF-8 UTF-8\n' >> /etc/locale.gen \
	&& locale-gen

# Set alias for easier work on console
RUN echo 'alias ll="ls -l --color=auto"' >> ~/.bashrc

# Install nodejs
RUN curl -sL https://deb.nodesource.com/setup_12.x  | bash - \
&& apt-get -y install nodejs \
&& npm install

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
&& composer --version

# Set timezone
RUN ln -snf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && echo ${TIMEZONE} > /etc/timezone \
&& printf '[PHP]\ndate.timezone = "%s"\n', ${TIMEZONE} > /usr/local/etc/php/conf.d/tzone.ini \
&& "date"

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/

# Type docker-php-ext-install to see available extensions
# requirements for laravel
RUN docker-php-ext-install pdo pdo_mysql mysqli mbstring tokenizer xml ctype json bcmath  \
# + some further
	zip curl iconv gd intl exif sodium soap calendar


# Install xdebug 2 + ssh2
RUN pecl install xdebug-2.9.8 ssh2-1.1.2 \
&& docker-php-ext-enable xdebug ssh2 \
&& pecl install mcrypt-1.0.2 \
&& docker-php-ext-enable mcrypt

# Cleanup
RUN apt-get clean && apt-get autoremove -y && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/src

WORKDIR /var/www/app
