FROM amazonlinux:2017.03
LABEL maintainer=youyo

RUN	yum install -y http://repo.zabbix.com/zabbix/3.4/rhel/6/x86_64/zabbix-release-3.4-1.el6.noarch.rpm && \
	yum install -y zabbix-server-mysql && \
	yumdownloader zabbix-server-mysql && \
	rpm -ivh --replacepkgs zabbix-server-mysql-*.rpm

ADD zabbix_server.conf /etc/zabbix/
EXPOSE 10051
CMD ["/usr/sbin/zabbix_server","--foreground","--config","/etc/zabbix/zabbix_server.conf"]
