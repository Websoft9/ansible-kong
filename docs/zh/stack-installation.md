# 初始化安装

在云服务器上部署 Kong 安装环境之后，请参考下面的步骤快速入门。

## 准备

1. 在云控制台获取您的 **服务器公网 IP 地址**
2. 在云控制台安全组中，检查 **Inbound（入）规则** 下的 **TCP:80** 端口是否开启
3. 若想用域名访问 Kong，请先到 **域名控制台** 完成一个域名解析

## Kong 安装向导

1. 验证 Kong 的安装状态
   ```
   curl -i -X GET --url http://kong:8001/services

   HTTP/1.1 200 OK
   Date: Sat, 22 Jan 2022 06:43:18 GMT
   Content-Type: application/json; charset=utf-8
   Connection: keep-alive
   Access-Control-Allow-Origin: *
   Content-Length: 23
   X-Kong-Admin-Latency: 234
   Server: kong/2.5.0
   ```

2. 使用本地电脑浏览器访问网址：*http://域名* 或 *http://服务器公网 IP*, 进入 Konga 管理创建界面
   ![Kong 登录页面](https://libs.websoft9.com/Websoft9/DocsPicture/zh/kong/kong-kongareg001-websoft9.png)

2. 创建管理员并登陆到 Konga 后台

3. 连接到 Kong Admin

> 需要了解更多 Kong 的使用，请参考官方文档：[Kong Documentation](https://www.kong.com/documentation.html)

## Kong 入门向导



## 常见问题

#### 浏览器打开 IP 地址，无法访问 Kong（白屏没有结果）？

您的服务器对应的安全组 80 端口没有开启（入规则），导致浏览器无法访问到服务器的任何内容

#### 本部署方案采用什么安装方式

Docker
