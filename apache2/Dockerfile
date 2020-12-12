FROM php:7.3-apache-buster

ENV DOCUMENT_ROOT $DOCUMENT_ROOT
ENV PHP_FPM_SOCKET $PHP_SOCKET

RUN \
  apt-get update && \
  apt-get install -y apache2 && \
  apt-get install -y libzip-dev && \
  apt-get install -y libxml2-dev && \
  apt-get install -y zlib1g-dev && \
  apt-get install -y libpng-dev && \
  apt-get install -y libfreetype6-dev && \
  apt-get install -y libjpeg62-turbo-dev && \
  apt-get install -y libicu-dev && \
  apt-get install -y libpspell-dev && \
  apt-get install -y libpq-dev && \
  apt-get install -y libldap2-dev && \
  apt-get install -y libxslt-dev && \
  docker-php-ext-install pgsql pdo pdo_pgsql && \
  docker-php-ext-install zip gd intl xmlrpc soap opcache && \
#   docker-php-ext-install soap zip intl pspell pgsql xsl pdo pdo_pgsql && \
#   docker-php-ext-configure opcache --enable-opcache && docker-php-ext-install opcache \
  a2enmod proxy && \
  a2enmod proxy_http && \
  a2enmod proxy_fcgi && \
  a2enmod authn_core && \
  a2enmod access_compat && \
  a2enmod alias && \
  a2enmod authz_core && \
  a2enmod authz_host && \
  a2enmod authz_user && \
  a2enmod dir && \
  a2enmod env && \
  a2enmod mime && \
  a2enmod reqtimeout && \
  a2enmod rewrite && \
  a2enmod status && \
  a2enmod filter && \
  a2enmod deflate && \
  a2enmod setenvif && \
  a2enmod vhost_alias && \
  a2enmod ssl && \
  apt-get autoremove -y && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists

RUN echo "${WEB_MY_TZ}" > /etc/timezone && \
    dpkg-reconfigure -f noninteractive tzdata

RUN ln -sf /dev/stderr /var/log/apache2/error.log

EXPOSE 80

CMD apachectl -D FOREGROUND