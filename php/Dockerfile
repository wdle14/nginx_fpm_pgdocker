FROM php:7.4-fpm-alpine
# Install Composer
RUN apk add --update \
		$PHPIZE_DEPS \
		freetype-dev \
		git \
		libjpeg-turbo-dev \
		libpng-dev \
		libxml2-dev \
		libzip-dev \
		openssh-client \
		php7-json \
		php7-openssl \
		php7-pdo \
		php7-pdo_mysql \
		php7-session \
		php7-simplexml \
		php7-tokenizer \
		php7-xml \
		imagemagick \
		imagemagick-libs \
		imagemagick-dev \
		php7-imagick \
		php7-pcntl \
		php7-zip \
		sqlite \
	&& docker-php-ext-install iconv soap sockets exif bcmath pdo_mysql pcntl \
	&& docker-php-ext-configure gd --with-jpeg --with-freetype \
	&& docker-php-ext-install gd \
	&& docker-php-ext-install zip

RUN printf "\n" | pecl install \
		imagick && \
		docker-php-ext-enable --ini-name 20-imagick.ini imagick

RUN printf "\n" | pecl install \
		pcov && \
		docker-php-ext-enable pcov

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
	&& php composer-setup.php \
	&& php -r "unlink('composer-setup.php');" \
	&& mv composer.phar /usr/bin/composer


RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

COPY yy-custom.ini /usr/local/etc/php/conf.d/

#ADD php.ini "/usr/local/etc/php/php.ini"

RUN \
    apk add --no-cache --virtual openssl-dev pcre-dev

RUN \
    pecl install redis && \
    pecl clear-cache && \
    docker-php-ext-enable redis && \
    docker-php-source delete

#RUN apk del --no-cache .build-deps $PHPIZE_DEPS && rm -rf /var/cache/apk/*



# add bash script
# RUN mkdir /script
# COPY run.sh /script/run.sh
# RUN chmod +x /script/run.sh
#ADD run.sh /
#WORKDIR /var/www/html/
#CMD bash -c "composer install"
#run internal command like composer & run supervisor
#ENTRYPOINT [ "/run.sh" ]
