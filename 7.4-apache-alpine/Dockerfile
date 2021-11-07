FROM alpine:3.14.2 AS builder

RUN apk update --no-cache \
    && apk add --no-cache curl ssmtp shadow \
        php7-apache2 php7-bcmath php7-bz2 php7-calendar php7-common php7-ctype php7-curl php7-dba \
        php7-dom php7-exif php7-ffi php7-fileinfo php7-ftp php7-gd php7-gettext php7-gmp php7-iconv php7-imap php7-intl \
        php7-json php7-ldap php7-mbstring php7-mysqli php7-mysqlnd php7-odbc php7-opcache php7-openssl php7-pcntl php7-pdo \
        php7-pdo_dblib php7-pdo_mysql php7-pdo_odbc php7-pdo_pgsql php7-pdo_sqlite php7-pear php7-pecl-igbinary php7-pecl-imagick \
        php7-pecl-mcrypt php7-pecl-memcached php7-pecl-mongodb php7-pecl-redis php7-pecl-ssh2 php7-pecl-timezonedb php7-pecl-yaml \
        php7-pecl-zmq php7-pgsql php7-phar php7-posix php7-session php7-simplexml php7-soap php7-sockets php7-sodium php7-sqlite3 \
        php7-static php7-sysvmsg php7-sysvsem php7-sysvshm php7-tidy php7-tokenizer php7-xml php7-xmlreader php7-xmlrpc php7-xmlwriter php7-xsl php7-zip

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
