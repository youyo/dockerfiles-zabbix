FROM centos:7
LABEL maintainer=youyo

ENV ZABBIX_MODULE_LINUX_EXTENDED 0.1.3

RUN	yum install -y http://repo.zabbix.com/zabbix/3.0/rhel/7/x86_64/zabbix-release-3.0-1.el7.noarch.rpm && \
	yum install -y zabbix-agent zabbix-get zabbix-sender && \
	mkdir /etc/zabbix/modules && \
	curl -sL https://github.com/youyo/zabbix-loadable-modules-linux-extended/releases/download/${ZABBIX_MODULE_LINUX_EXTENDED}/linux-extended.so -o /etc/zabbix/modules/linux-extended.so

ADD zabbix_agentd.conf /etc/zabbix/
EXPOSE 10050
CMD ["/usr/sbin/zabbix_agentd","--foreground","--config","/etc/zabbix/zabbix_agentd.conf"]
