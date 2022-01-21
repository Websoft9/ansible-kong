# 服务启停

使用由 Websoft9 提供的 Kong 部署方案，可能需要用到的服务如下：

### Kong

```shell
sudo systemctl start kong-elasticsearch | kong-logstash | kong-kibana
sudo systemctl stop kong-elasticsearch | kong-logstash | kong-kibana
sudo systemctl restart kong-elasticsearch | kong-logstash | kong-kibana
sudo systemctl status kong-elasticsearch | kong-logstash | kong-kibana
```

### Docker

```shell
sudo systemctl start docker
sudo systemctl restart docker
sudo systemctl stop docker
sudo systemctl status docker
```

### Docker-Compose

```
#创建容器编排
sudo docker-compose up -d

#删除容器编排
sudo docker-compose up -d

#启动/停止/重启
sudo docker-compose start
sudo docker-compose stop
sudo docker-compose restart
```

### Nginx

```shell
sudo systemctl start nginx
sudo systemctl stop nginx
sudo systemctl restart nginx
sudo systemctl status nginx
```
