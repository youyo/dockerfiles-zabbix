FROM centos:7 AS build-env
LABEL maintainer=youyo

RUN	yum install -y http://repo.zabbix.com/zabbix/3.0/rhel/7/x86_64/zabbix-release-3.0-1.el7.noarch.rpm && \
	yum install -y \
		zabbix-web-mysql \
		zabbix-web-japanese

FROM centos:7
LABEL maintainer=youyo

RUN	yum install -y https://rpms.remirepo.net/enterprise/remi-release-7.rpm && \
	yum-config-manager --enable remi-php71 && \
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
