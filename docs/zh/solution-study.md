# Kong 速学

## Kong Stack

“Kong” 是三个开源项目的缩写：Elasticsearch，Logstash 和 Kibana。 Elasticsearch 是搜索和分析引擎。

- Elasticsearch 是一个存储数据和检索数据等数据库
- Logstash 是数据提取、清洗和整理的中间件
- Kibana 是 Elasticsearch 的可视化管理分析界面

另外，随着 Elastic 公司不断发展，他们把更多的产品加入到了 Kong 家族，例如：一个日志采集工具 Beats

下面是 Kong 用于日志场景的典型架构图

![](https://libs.websoft9.com/Websoft9/DocsPicture/zh/kong/kong-arch001-websoft9.png)

## 认证

Elastic Stack 的[安全](https://elasticstack.blog.csdn.net/article/details/100548174)是由 x-pack 所提供的。在 Elastic Stack 7.0 版本之前，这个是商用的版本，需要进行安装，并购买。从 Elastic Stack 7.0 之后，x-pack 都已经在发布版中，所以不需要进行安装。我们只需要进行配置就可以了。

Elasticsearch 配置文件中启动下面的项，即开启账号密码认证。

```
xpack.security.enabled: true
```

Elasticsearch 镜像支持用户名和密码的环境变量，因此非常方便设置。 Elasticsearch 设置认证后，Kibana 和 Logstash 对应的认证处理方式如下：

- Kibana：镜像提供 **ELASTICSEARCH_USERNAME** 和 **ELASTICSEARCH_PASSWORD** 两个环境变量参数
- Logstash：
