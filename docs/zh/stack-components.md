---
sidebarDepth: 3
---

# 参数

Kong 预装包包含 Kong 运行所需一序列支撑软件（简称为“组件”），下面列出主要组件名称、安装路径、配置文件地址、端口、版本等重要的信息。

## 路径

本部署方案中的 Kong 采用 Docker 部署，运行 `docker ps` 查看运行的容器。

```
CONTAINER ID   IMAGE               COMMAND                  CREATED       STATUS                 PORTS                                                                                                                          NAMES
c5b7dedcbffc   pantsel/konga       "/app/start.sh"          2 hours ago   Up 2 hours             0.0.0.0:9004->1337/tcp, :::9004->1337/tcp                                                                                      kong-konga
539733eb1cfd   kong:latest         "/docker-entrypoint.…"   2 hours ago   Up 2 hours (healthy)   0.0.0.0:8000-8001->8000-8001/tcp, :::8000-8001->8000-8001/tcp, 0.0.0.0:8443-8444->8443-8444/tcp, :::8443-8444->8443-8444/tcp   kong
804a39757ad9   postgres:9.6        "docker-entrypoint.s…"   2 hours ago   Up 2 hours             0.0.0.0:5432->5432/tcp, :::5432->5432/tcp                                                                                      kong-database
```

### Kong

Kong Stack 包含：Kong, Konga, Postgres 等组件

Kong 安装目录： */data/wwwroot/kong*  
Kong 配置容器配置文件： */data/wwwroot/kong/.env*

### Nginx

Nginx 虚拟主机配置文件：*/etc/nginx/conf.d/default.conf*  
Nginx 主配置文件： */etc/nginx/nginx.conf*  
Nginx 日志文件： */var/log/nginx*  
Nginx 伪静态规则目录： */etc/nginx/conf.d/rewrite*  
Nginx 验证访问文件：*/etc/nginx/.htpasswd/htpasswd.conf*  

### Docker

Docker 根目录: */var/lib/docker*  
Docker 镜像目录: */var/lib/docker/image*  
Docker daemon.json 文件：默认没有创建，请到 _/etc/docker_ 目录下根据需要自行创建

## 端口号

在云服务器中，通过 **[安全组设置](https://support.websoft9.com/docs/faq/zh/tech-instance.html)** 来控制（开启或关闭）端口是否可以被外部访问。

通过命令`netstat -tunlp` 看查看相关端口，下面列出可能要用到的端口：

| 类型          | 端口号 | 用途                         | 必要性 |
| ------------- | ------ | ---------------------------- | ------ |
| Nginx | 80   | Nginx 端口           | 可选   |
| Konga        | 9001   | 通过 HTTP 访问 Konga 控制台 | 可选   |
| Postgre | 5432   | Postgre 数据库端口            | 可选   |
| Kong      | 8000   | Proxy                 | 可选   |
| Kong      | 8443   | Proxy SSL                 | 可选   |
| Kong       | 8001  | Admin API                 | 可选   |
| Kong      | 8444   | Admin API SSL                 | 可选   |

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
