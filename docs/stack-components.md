---
sidebarDepth: 3
---

# Parameters

The Kong deployment package contains a sequence of software (referred to as "components") required for Kong to run. Below list the important information, the component name, installation directory path, configuration file path, port, version, etc.

## Path

This solution use Docker to deploy all service, you can run the command `docker ps` to list them

### Kong

Kong installation directory:  */data/kong*  
Kong logs directory:  */data/logs/kong*

### Apache

Apache vhost configuration file: _/etc/httpd/conf.d/vhost.conf_  
Apache main configuration file: _/etc/httpd/conf/httpd.conf_  
Apache logs file: _/var/log/httpd_  
Apache module configuration file: _/etc/httpd/conf.modules.d/00-base.conf_

### Nginx

Nginx vhost configuration file: _/etc/nginx/conf.d/default.conf_  
Nginx main configuration file: _/etc/nginx/nginx.conf_  
Nginx logs file: _/var/log/nginx_  
Nginx rewrite rules directory: _/etc/nginx/conf.d/rewrite_  
Nginx htpasswd file: _/etc/nginx/.htpasswd/htpasswd.conf_

### MySQL

MySQL installation directory: _/usr/local/mysql_  
MySQL data directory: _/data/mysql_  
MySQL configuration file: _/etc/my.cnf_

MySQL Web Management refer to [MySQL Management](/admin-mysql.md)

### MySQL on Docker

MySQL data directory: _/data/db/mysql/data_  
MySQL log directory: _/data/db/mysql/logs_

### phpMyAdmin

phpMyAdmin is a visual MySQL management tool, is installed based on docker.

phpMyAdmin directory：_/data/apps/phpmyadmin_  
phpMyAdmin docker compose file：_/data/apps/phpmyadmin/docker-compose.yml_

### PostgreSQL

PostgreSQL data directory: _/data/postgresql/pgdata_  
PostgreSQL configuration directory: _/data/postgresql/config_  
PostgreSQL logs directory: _/data/postgresql/log_

> The above list is the directory created by soft link, please query more file path information through commands like `locate pg_hba.conf`

### PostgreSQL on Docker

PostgreSQL data directory: _/data/db/postgresql/data_  
PostgreSQL data directory: _/data/db/postgresql/logs_

### pgAdmin

pgAdmin is a visual PostgreSQL management tool, is installed based on docker.

pgAdmin directory：_/data/apps/pgadmin_  
pgAdmin docker compose file：_/data/apps/pgadmin/docker-compose.yml_

### MongoDB

MongoDB data directory: _/var/lib/mongodb_  
MongoDB Configuration File:  */etc/mongod.conf*  
MongoDB logs File: _/var/log/mongodb_

### adminMongo

adminMongo is a visual MongoDB management tool, is installed based on docker.

adminMongo directory：_/data/apps/adminmongo_  
adminMongo docker compose file：_/data/apps/adminmongo/docker-compose.yml_

### Docker

Docker root directory: */var/lib/docker*  
Docker image directory: */var/lib/docker/image*  
Docker daemon.json: please create it when you need and save to to the directory _/etc/docker_

### Redis

Redis configuration file: _/etc/redis.conf_  
Redis data directory: _/var/lib/redis_  
Redis logs file: _/var/log/redis/redis.log_

## Ports

Open or close ports by **[Security Group Setting](https://support.websoft9.com/docs/faq/tech-instance.html)** of your Cloud Server to decide whether the port can be accessed from Internet.

You can run the cmd `netstat -tunlp` to check all related ports.

The following are the ports you may use:

| Name | Number | Use                            | Necessity |
| ---- | ------ | ------------------------------ | --------- |
| TCP  | 80     | HTTP to access Kong            | Required  |
| TCP  | 443    | HTTPS to access Kong           | Optional  |
| TCP  | 3306   | Remote to access MySQL         | Optional  |
| TCP  | 9003   | Use port to access Kong        | Optional  |
| TCP  | 9002   | Kong Document Server on Docker | Optional  |
| TCP  | 9090   | phpMyAdmin on Docker           | Optional  |

## Version

You can see the version on product pages at Marketplace. However, after being deployed to your server, the components will be updated automatically, resulting in a certain change in the version number. Therefore, run the command on the server to view the exact version number.

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
