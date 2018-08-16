# docker-compose-file

### 防火墙设置
1. 关闭宿主机的防火墙：systemctl stop firewalld.service,
2. 查看防火墙状态：firewall-cmd --state
3. 禁用防火墙：systemctl disable firewalld.service

### docker容器设置
1. 设置开机启动：systemctl enable docker

### docker常用用命令
https://github.com/xjzrc/Linux-Tutorial/blob/master/markdown-file/Docker-Install-And-Usage.md

### kafka
1. docker-compose中KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://192.168.138.110:9093要使用宿主机IP地址
