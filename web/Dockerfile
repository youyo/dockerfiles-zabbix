FROM amazonlinux:2017.03 AS build-env
LABEL maintainer=youyo

RUN	yum install -y http://repo.zabbix.com/zabbix/3.4/rhel/6/x86_64/zabbix-release-3.4-1.el6.noarch.rpm && \
	yum install -y \
		zabbix-web-mysql \
		zabbix-web-japanese

FROM amazonlinux:2017.03
LABEL maintainer=youyo

RUN	yum install -y https://rpms.remirepo.net/enterprise/remi-release-6.rpm && \
	yum-config-manager --enable remi remi-php71 epel && \
	yum-config-manager --save --setopt='remi.priority=1' && \
	yum-config-manager --save --setopt='remi-php71.priority=1' && \
	yum-config-manager --save --setopt='epel.priority=1' && \
	yum install -y \
		httpd \
		fontpackages-filesystem \
		dejavu-fonts-common \
		dejavu-sans-fonts \
		vlgothic-p-fonts \
		php \
		php-common \
		php-mcrypt \
		php-opcache \
		php-mbstring \
		php-pear \
		php-process \
		php-xml \
		php-pdo \
		php-mysqlnd \
		php-gd \
		php-bcmath \
		php-xmlrpc \
		php-fpm

COPY --from=build-env /etc/zabbix /etc/zabbix
COPY --from=build-env /usr/share/zabbix /var/www/html/zabbix
ADD zabbix.conf.php /etc/zabbix/web/zabbix.conf.php
ADD httpd.conf /etc/httpd/conf/httpd.conf

RUN chown -R apache: /etc/zabbix/web/ && \
	ln -sf /usr/share/fonts/vlgothic/VL-PGothic-Regular.ttf /var/www/html/zabbix/fonts/graphfont.ttf && \
	localedef -f UTF-8 -i ja_JP ja_JP

EXPOSE 80
CMD ["/usr/sbin/httpd","-DFOREGROUND"]
