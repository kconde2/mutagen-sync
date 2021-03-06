FROM php:7.3-apache

## Basic tools
RUN apt-get update -y && \
  apt-get upgrade -y && \
  apt-get install -y bash \
  apt-utils \
  curl \
  wget \
  ca-certificates \
  nano \
  git \
  unzip \
  libicu-dev \
  zlib1g-dev \
  libxml2 \
  libxml2-dev \
  libreadline-dev \
  libzip-dev \
  gnupg \
  && docker-php-ext-install \
  pdo_mysql \
  opcache \
  intl \
  zip \
  && rm -fr /tmp/* && \
  rm -rf /var/list/apt/* && \
  rm -r /var/lib/apt/lists/* && \
  apt-get clean && \
  a2enmod rewrite ssl

## Composer
ENV COMPOSER_ALLOW_SUPERUSER=1
RUN echo "memory_limit = -1" > /usr/local/etc/php/conf.d/memory_limit.ini; \
    curl -sS http://getcomposer.org/installer | php -- --filename=composer && chmod a+x composer  && mv composer /usr/local/bin/composer; \
    echo 'export PATH=~/.composer/vendor/bin:$PATH' >> ~/.bashrc; \
    composer global require hirak/prestissimo

## NodeJS
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash && \
    apt-get install -y nodejs

## Yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && \
    apt-get install yarn

# gd
RUN apt-get update \
    && apt-get install -y \
	    libfreetype6-dev \
	    libpng-dev \
	    libjpeg-dev \
    && docker-php-ext-configure gd \
	    --with-freetype-dir=/usr/include/ \
	    --with-jpeg-dir=/usr/include/ \
	    --with-png-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) \
	    gd \
    && apt-get purge -y \
	    libfreetype6-dev \
	    libpng-dev \
	    libjpeg-dev

WORKDIR /var/www/html

# Add a non-root user to prevent files being created with root permissions on host machine.
ARG PUID=1000
ENV PUID ${PUID}
ARG PGID=1000
ENV PGID ${PGID}

RUN groupmod -o -g ${PGID} www-data && \
    usermod -o -u ${PUID} -g www-data www-data

EXPOSE 80
