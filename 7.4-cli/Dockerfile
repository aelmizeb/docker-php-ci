FROM php:7.4-cli-buster

MAINTAINER "Abdellatif EL MIZEB" <aelmizeb@gmail.com>

ARG DEBIAN_FRONTEND=noninteractive

ENV COMPOSER_ALLOW_SUPERUSER 1

ARG MAGENTO2_PUB
ENV MAGENTO2_PUB $MAGENTO2_PUB

ARG MAGENTO2_PRI
ENV MAGENTO2_PRI $MAGENTO2_PRI

ENV FORCE_FULL_BUILD 20200716

RUN echo "FORCE_FULL_BUILD : $FORCE_FULL_BUILD"
RUN echo "MAGENTO2_PUB : $MAGENTO2_PUB"
RUN echo "MAGENTO2_PRI : $MAGENTO2_PRI"

RUN \
    apt-get update \
    && apt-get install -y \
        libfreetype6-dev libicu-dev libjpeg62-turbo-dev libmcrypt-dev libpng-dev libxml2-utils libxslt-dev libzip-dev \
    && apt-get clean autoclean autoremove -y \
    && rm -rf /var/lib/apt/lists/*

RUN \
    echo "memory_limit=1024M" > /usr/local/etc/php/conf.d/php.ini \
    && echo "phar.readonly=Off" >> /usr/local/etc/php/conf.d/php.ini

RUN \
    pecl install mcrypt redis xdebug \
    && docker-php-ext-enable mcrypt redis xdebug \
    && docker-php-ext-install bcmath gd gettext iconv intl pdo_mysql soap sockets xsl zip

RUN \
    mkdir -p ~/.ssh \
    && chmod 700 ~/.ssh \
    && echo "" > ~/.ssh/known_hosts \
    && echo "Host *\n  StrictHostKeyChecking no\n  UserKnownHostsFile=/dev/null\n  LogLevel ERROR" > ~/.ssh/config

RUN \
    apt-get update \
    && apt-get install -y \
        ack-grep bash bsdmainutils dos2unix gettext git gnupg graphviz jq moreutils nano python python3 python-pip python3-pip shellcheck sshpass rsync tree unzip zip \
        python-dev python3-dev \
    && apt-get clean autoclean autoremove -y \
    && rm -rf /var/lib/apt/lists/*

RUN \
    curl -sL -o /usr/local/bin/composer https://getcomposer.org/download/1.10.1/composer.phar \
    && chmod +x /usr/local/bin/composer

RUN \
    curl -sL -o /usr/local/bin/jsawk http://github.com/micha/jsawk/raw/master/jsawk \
    && chmod +x /usr/local/bin/jsawk
    
RUN \
    curl -sL -o /usr/local/bin/slack https://raw.githubusercontent.com/rockymadden/slack-cli/master/src/slack \
    && chmod +x /usr/local/bin/slack

RUN \
    pip install awscli yq

RUN \
    curl -sL -o /usr/local/bin/php-cs-fixer https://cs.symfony.com/download/php-cs-fixer-v2.phar \
    && chmod +x /usr/local/bin/php-cs-fixer
   
RUN \
    curl -sL -o /usr/local/bin/validate_m2_package https://raw.githubusercontent.com/magento/marketplace-tools/master/validate_m2_package.php \
    && sed -i '1s/^.*$/#!\/usr\/bin\/env php/' /usr/local/bin/validate_m2_package \
    && chmod +x /usr/local/bin/validate_m2_package
    
RUN \
    curl -sL https://deb.nodesource.com/setup_10.x | bash \
    && apt-get install -y nodejs \
    && apt-get clean autoclean autoremove -y \
    && rm -rf /var/lib/apt/lists/*

RUN \
    mkdir -p ~/eslint/standard ~/eslint/semistandard \
    && npm install -g bower csslint eslint gulp grunt jshint jslint semistandard standard stylelint \
    && npm install -g eslint-plugin-import eslint-plugin-node eslint-plugin-promise eslint-plugin-standard \
    && npm install -g eslint-config-standard eslint-config-semistandard \
    && npm install -g stylelint-config-standard \
    && npm install -g jsonlint yaml-lint \
    && echo '{"extends": ["standard"]}' > ~/eslint/standard/.eslintrc.json \
    && echo '{"extends": ["semistandard"]}' > ~/eslint/semistandard/.eslintrc.json