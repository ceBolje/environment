FROM registry.lavaimagem.net/docker/ubuntu:18.04

LABEL description="Php5.6-fpm image" \
    maintainer="Rudi Servo <rudi.servo@lavaimagem.com" \
    vendor=Lavaimagem \
    name="net.lavaimagem.registry/docker/php-5.6-fpm-bionic"


ENV TIMEZONE=UTC \
    LANGUAGE=en_US.UTF-8 \
    LANG=en_US.UTF-8 \
    LC_ALL=en_US.UTF-8 \
    DEBIAN_FRONTEND=noninteractive \
    TERM=xterm \
    PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

RUN apt clean -y \
    && apt-get update -y \
    && apt-get upgrade -y \
    && apt-get install --no-install-recommends -yq \
        php5.6 \
        php5.6-bcmath \
        php5.6-bz2 \
        php5.6-cgi \
        php5.6-cli \
        php5.6-common \
        php5.6-curl \
        php5.6-dba \
        php5.6-dev \
        php5.6-enchant \
        php5.6-fpm \
        php5.6-gd \
        php5.6-gmp \
        php5.6-imap \
        php5.6-interbase \
        php5.6-intl \
        php5.6-json \
        php5.6-ldap \
        php5.6-mbstring \
        php5.6-mcrypt \
        php5.6-mysql \
        php5.6-odbc \
        php5.6-opcache \
        php5.6-pgsql \
        php5.6-phpdbg \
        php5.6-pspell \
        php5.6-readline \
        php5.6-recode \
        php5.6-soap \
        php5.6-sqlite3 \
        php5.6-sybase \
        php5.6-tidy \
        php5.6-xml \
        php5.6-xmlrpc \
        php5.6-xsl \
        php5.6-zip \
        php-xdebug \
    && apt-get autoremove -y \
    && apt-get clean -y \
    && phpenmod mysql \
    && rm -rf /tmp/* /var/tmp/* \
    && find /var/cache/apt/archives /var/lib/apt/lists -not -name lock -type f -delete \
    && find /var/cache -type f -delete \
    && find /var/log -type f | while read f; do echo -n '' > ${f}; done

RUN sed -i "s/;date.timezone =.*/date.timezone = UTC/" /etc/php/5.6/cli/php.ini
RUN sed -i "s/;date.timezone =.*/date.timezone = UTC/" /etc/php/5.6/fpm/php.ini
RUN sed -i "s/display_errors = Off/display_errors = On/" /etc/php/5.6/fpm/php.ini
RUN sed -i "s/upload_max_filesize = .*/upload_max_filesize = 10M/" /etc/php/5.6/fpm/php.ini
RUN sed -i "s/post_max_size = .*/post_max_size = 12M/" /etc/php/5.6/fpm/php.ini
RUN sed -i "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/" /etc/php/5.6/fpm/php.ini
RUN sed -i -e "s/pid =.*/pid = \/var\/run\/php5.6-fpm.pid/" /etc/php/5.6/fpm/php-fpm.conf
RUN sed -i -e "s/error_log =.*/error_log = \/proc\/self\/fd\/2/" /etc/php/5.6/fpm/php-fpm.conf
RUN sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php/5.6/fpm/php-fpm.conf
RUN sed -i "s/listen = .*/listen = 9000/" /etc/php/5.6/fpm/pool.d/www.conf
RUN sed -i "s/;catch_workers_output = .*/catch_workers_output = yes/" /etc/php/5.6/fpm/pool.d/www.conf
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN apt-get update && apt-get install -y git


WORKDIR /var/htdocs

expose 9000
CMD ["php-fpm5.6"]
