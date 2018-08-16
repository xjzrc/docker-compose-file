# docker-compose-file
1.
关闭宿主机的防火墙：systemctl stop firewalld.service,
查看防火墙状态：firewall-cmd --state
禁用防火墙：systemctl disable firewalld.service

2.kafka-docker-compose中KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://192.168.138.110:9093要使用宿主机IP地址
