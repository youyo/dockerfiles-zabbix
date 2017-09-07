FROM centos:7
LABEL maintainer=youyo

RUN	yum install -y http://repo.zabbix.com/zabbix/3.4/rhel/7/x86_64/zabbix-release-3.4-2.el7.noarch.rpm && \
	yum install -y zabbix-agent zabbix-get zabbix-sender && \
	mkdir /etc/zabbix/modules

ADD zabbix_agentd.conf /etc/zabbix/
EXPOSE 10050
CMD ["/usr/sbin/zabbix_agentd","--foreground","--config","/etc/zabbix/zabbix_agentd.conf"]
