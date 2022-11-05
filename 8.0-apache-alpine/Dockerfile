FROM alpine:3.14 AS builder

RUN apk update --no-cache \
    && apk add --no-cache curl ssmtp shadow \
        php8-apache2 php8-bcmath php8-bz2 php8-calendar php8-common php8-ctype php8-curl php8-dba \
        php8-dom php8-exif php8-ffi php8-fileinfo php8-ftp php8-gd php8-gettext php8-gmp php8-iconv php8-imap php8-intl \
        php8-json php8-ldap php8-mbstring php8-mysqli php8-mysqlnd php8-odbc php8-opcache php8-openssl php8-pcntl php8-pdo \
        php8-pdo_dblib php8-pdo_mysql php8-pdo_odbc php8-pdo_pgsql php8-pdo_sqlite php8-pear php8-pecl-igbinary php8-pecl-imagick \
        php8-pecl-mcrypt php8-pecl-memcached php8-pecl-mongodb php8-pecl-redis php8-pecl-ssh2 php8-pecl-timezonedb php8-pecl-yaml \
        php8-pgsql php8-phar php8-posix php8-session php8-simplexml php8-soap php8-sockets php8-sodium php8-sqlite3 \
        php8-sysvmsg php8-sysvsem php8-sysvshm php8-tidy php8-tokenizer php8-xml php8-xmlreader php8-xmlwriter php8-xsl php8-zip

RUN ln -sf /proc/self/fd/2 /var/log/apache2/access.log && \
    ln -sf /proc/self/fd/2 /var/log/apache2/error.log && \
    mkdir -p /var/www/html && \
    adduser -S -s /sbin/nologin -G www-data -h /var/www/html www-data

COPY --from=composer /usr/bin/composer /usr/bin/composer
COPY entrypoint.sh /
RUN chmod +x /entrypoint.sh

WORKDIR /var/www/html
VOLUME [ "/var/www/html" ]
EXPOSE 80
ENTRYPOINT [ "/entrypoint.sh" ]
CMD [ "httpd", "-DFOREGROUND" ]
