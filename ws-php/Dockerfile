FROM cloud9/workspace
MAINTAINER Cloud9 IDE, inc. <info@c9.io>

ADD ./files/home /home/ubuntu

RUN bash -c 'chmod -R g+w /home/ubuntu/{workspace,sessions} && \
    chown -R ubuntu:ubuntu /home/ubuntu/{workspace,sessions}'

# PHP based on defaults from
#   http://docs.travis-ci.com/user/ci-environment/#Extensions
#   https://devcenter.heroku.com/articles/php-support
# Xdebug, most recent PECL version
ADD ./files/etc/php7 /etc/php7
RUN apt-get install -y php5 php7-cli php5-fpm \
        php7-curl php7-gd php7-json php7-pgsql php7-readline php7-sqlite \
        php7-tidy php7-xmlrpc php7-xsl php7-intl php7-mcrypt php7-mysqlnd \
        php-pear \
    && apt-get install -y php7-dev \
        && pecl install xdebug \
        && php7enmod xdebug \
    && cd /etc/php7/mods-available && ls *.ini | sed 's/\.ini$//' | xargs php7enmod
RUN chown -R ubuntu: /home/ubuntu/lib
