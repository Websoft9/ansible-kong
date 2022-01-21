---
sidebarDepth: 3
---

# 参数

Kong 预装包包含 Kong 运行所需一序列支撑软件（简称为“组件”），下面列出主要组件名称、安装路径、配置文件地址、端口、版本等重要的信息。

## 路径

本部署方案中的 Kong 采用 Docker 部署，运行 `docker ps` 查看运行的容器。

```
CONTAINER ID   IMAGE                  COMMAND                  CREATED         STATUS         PORTS                                                                                                                                                                        NAMES
4c27ee6b8e98   logstash:7.13.4        "/usr/local/bin/dock…"   4 minutes ago   Up 4 minutes   0.0.0.0:5000->5000/tcp, :::5000->5000/tcp, 0.0.0.0:5044->5044/tcp, :::5044->5044/tcp, 0.0.0.0:9600->9600/tcp, 0.0.0.0:5000->5000/udp, :::9600->9600/tcp, :::5000->5000/udp   kong-logstash
babdf8193e8d   kibana:7.13.4          "/bin/tini -- /usr/l…"   4 minutes ago   Up 4 minutes   0.0.0.0:9001->5601/tcp, :::9001->5601/tcp                                                                                                                                    kong-kibana
de14eb80b9f9   elasticsearch:7.13.4   "/bin/tini -- /usr/l…"   4 minutes ago   Up 4 minutes   0.0.0.0:9200->9200/tcp, :::9200->9200/tcp, 0.0.0.0:9300->9300/tcp, :::9300->9300/tcp                                                                                         kong-elasticsearch
```

### Kong

Kong Stack 包含：Elasticsearch, Kibana, Logstash 等组件

Kong 安装目录： */data/wwwroot/kong*  
Kong 配置目录： */data/wwwroot/kong/src*  
Kong 配置容器配置文件： */data/wwwroot/kong/.env*

### Nginx

Nginx 虚拟主机配置文件：_/etc/nginx/conf.d/default.conf_  
Nginx 主配置文件： _/etc/nginx/nginx.conf_  
Nginx 日志文件： _/var/log/nginx_  
Nginx 伪静态规则目录： _/etc/nginx/conf.d/rewrite_  
Nginx 验证访问文件：_/etc/nginx/.htpasswd/htpasswd.conf_

### Docker

Docker 根目录: */var/lib/docker*  
Docker 镜像目录: */var/lib/docker/image*  
Docker daemon.json 文件：默认没有创建，请到 _/etc/docker_ 目录下根据需要自行创建

## 端口号

在云服务器中，通过 **[安全组设置](https://support.websoft9.com/docs/faq/zh/tech-instance.html)** 来控制（开启或关闭）端口是否可以被外部访问。

通过命令`netstat -tunlp` 看查看相关端口，下面列出可能要用到的端口：

| 类型          | 端口号 | 用途                         | 必要性 |
| ------------- | ------ | ---------------------------- | ------ |
| Kibana        | 9001   | 通过 HTTP 访问 Kibana 控制台 | 可选   |
| Elasticsearch | 9200   | Elasticsearch HTTP           | 可选   |
| Elasticsearch | 9300   | Elasticsearch TCP            | 可选   |
| Logstash      | 9600   | Logstash API                 | 可选   |
| Logstash      | 5000   | Logstash TCP                 | 可选   |
| Logstash      | 5044   | Logstash TCP                 | 可选   |

## 版本号

组件版本号可以通过云市场商品页面查看。但部署到您的服务器之后，组件会自动进行更新导致版本号有一定的变化，故精准的版本号请通过在服务器上运行命令查看：

```shell
# Check all components version
sudo cat /data/logs/install_version.txt

# Linux Version
lsb_release -a

# Nginx  Version
nginx -V

# Docker Version
docker -v

# Kong version
docker exec -it kong-elasticsearch bin/elasticsearch --version
```
