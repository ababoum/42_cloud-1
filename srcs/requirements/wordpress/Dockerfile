FROM alpine:3.17.2

RUN apk update --no-cache --no-progress && \
	apk upgrade --no-cache --no-progress 

RUN apk add --no-cache --no-progress php php-fpm \
	php-mysqli php-json php-phar php-iconv php-mbstring \
	mariadb-client

RUN	sed -i 's/listen = 127\.0\.0\.1:9000/listen = 9000/g' /etc/php81/php-fpm.d/www.conf


RUN mkdir -p /var/www/html
RUN chown -R root:root /var/www/html/
RUN wget https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
RUN chmod +x wp-cli.phar
RUN mv wp-cli.phar /usr/local/bin/wp
COPY ./tools/auto_config.sh /usr/bin/auto_config.sh
RUN chmod +x /usr/bin/auto_config.sh
RUN apk add --no-cache util-linux

ENTRYPOINT [ "auto_config.sh" ]
CMD ["/usr/sbin/php-fpm81", "-F"]
