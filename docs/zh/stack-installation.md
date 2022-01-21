# 初始化安装

在云服务器上部署 Kong 安装环境之后，请参考下面的步骤快速入门。

## 准备

1. 在云控制台获取您的 **服务器公网 IP 地址**
2. 在云控制台安全组中，检查 **Inbound（入）规则** 下的 **TCP:80** 端口是否开启
3. 若想用域名访问 Kong，请先到 **域名控制台** 完成一个域名解析
4. 登录云服务器，运行下面的命令，拉取 Kong 相关 Docker 镜像并启动容器

   ```
   cd /data/wwwroot/kong && docker-compose pull && docker-compose up -d
   ```

   > Elastic 开源版 License 不允许第三方的分发行为，但允许用户免费使用，故需自行获取镜像。

## Kong 安装向导

1. 使用本地电脑浏览器访问网址：_http://域名_ 或 _http://服务器公网 IP_, 进入 Kong 登录界面
   ![Kong 登录页面](https://libs.websoft9.com/Websoft9/DocsPicture/zh/kong/kong-login-websoft9.png)

2. 输入账号密码（[不知道账号密码？](/zh/stack-accounts.md#kong)），成功登录到 Kong 后台  
   ![Kong 后台](https://libs.websoft9.com/Websoft9/DocsPicture/zh/kong/kong-bkreminder-websoft9.png)
   ![Kong 控制台](https://libs.websoft9.com/Websoft9/DocsPicture/zh/kong/kong-dashboard-websoft9.png)

> 需要了解更多 Kong 的使用，请参考官方文档：[Kong Documentation](https://www.kong.com/documentation.html)

## Kong 入门向导

Kong 的数据源多种多样，这里用常见的日志文件为 Logstash 的输入为例，步骤如下：

1. 在 Logstash 的配置文件 logstash.conf 设置索引"mytest"，并重启容器

```
input{
    file{
        path => "/var/log/yum.log"
        type => "elasticsearch"
        start_position => "beginning"
    }
}

output {
	elasticsearch {
		hosts => "elasticsearch:9200"
		user => "elastic"
		password => "elastic123"
                index => "mytest"
	}
}
```

2. 验证 Elasticsearch 和 Logstash 是否成功连接，索引数据是否生效(通过 URL 验证：http://服务器公网 IP:9200/\_cat/indices?v)

![Kong 验证](https://libs.websoft9.com/Websoft9/DocsPicture/zh/kong/kong-wizardindex-websoft9.png)

3. 登陆 Kibana，点击【Manage】，再点击右侧菜单的【Index Patterns】

![Kong Index](https://libs.websoft9.com/Websoft9/DocsPicture/zh/kong/kong-wizard1-websoft9.png)

![Kong Index](https://libs.websoft9.com/Websoft9/DocsPicture/zh/kong/kong-wizard2-websoft9.png)

![Kong Index](https://libs.websoft9.com/Websoft9/DocsPicture/zh/kong/kong-wizard3-websoft9.png)

4. 检索"mytest"，根据提示完成创建

![Kong Index](https://libs.websoft9.com/Websoft9/DocsPicture/zh/kong/kong-wizard4-websoft9.png)

![Kong Index](https://libs.websoft9.com/Websoft9/DocsPicture/zh/kong/kong-wizard5-websoft9.png)

5. 索引在 Kibana 创建成功，可以用时间条件在此检索数据

![Kong Index](https://libs.websoft9.com/Websoft9/DocsPicture/zh/kong/kong-wizard6-websoft9.png)

![Kong Index](https://libs.websoft9.com/Websoft9/DocsPicture/zh/kong/kong-wizard7-websoft9.png)

## 常见问题

#### 浏览器打开 IP 地址，无法访问 Kong（白屏没有结果）？

您的服务器对应的安全组 80 端口没有开启（入规则），导致浏览器无法访问到服务器的任何内容

#### 本部署方案采用什么安装方式

Docker
