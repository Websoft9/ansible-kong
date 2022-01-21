# 更多...

下面每一个方案，都经过实践证明行之有效，希望能够对你有帮助

## 配置

Kong 目录下提供了 Kong Stack 各个组件的配置文件，用户可以修改配置文件，然后重启容器即可

## 域名绑定

绑定域名的前置条件是：已经完成域名解析（登录域名控制台，增加一个 A 记录指向服务器公网 IP）

完成域名解析后，从服务器安全和后续维护考量，需要完成**域名绑定**：

Kong 域名绑定操作步骤：

1. 确保域名解析已经生效
2. 使用 SFTP 工具登录云服务器
3. 修改 [Nginx 虚拟机主机配置文件](/zh/stack-components.md#nginx)，将其中的 **server_name** 项的值修改为你的域名
   ```text
   server
   {
   listen 80;
   server_name kong.yourdomain.com;  # 此处修改为你的域名
   ...
   }
   ```
4. 保存配置文件，重启 [Nginx 服务](/zh/admin-services.md#nginx)

## 重置密码

常用的 Kong 重置密码相关的操作主要有修改密码和找回密码两种类型：

### 修改密码

登录 Kibana 后，右上角用户图标的【用户配置文件】即可修改密码

### 找回密码

如果用户忘记了密码，需通过重新运行容器的方式重置密码：

```
cd /data/wwwroot/kong
docker-compose down && docker-compose up -d
```

`.env`文件中的 **DB_ES_PASSWORD** 变量即重置后的密码
