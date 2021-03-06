# 故障处理

此处收集使用 Kong 过程中最常见的故障，供您参考

> 大部分故障与云平台密切相关，如果你可以确认故障的原因是云平台造成的，请参考[云平台文档](https://support.websoft9.com/docs/faq/zh/tech-instance.html)

#### 如何查看错误日志？

日志文件路径为：`/data/logs`。检索关键词 **Failed** 或者 **error** 查看错误

#### Kong 服务无法启动？

服务无法启动最常见的问题包括：磁盘空间不足，内存不足，配置文件错误。  
建议先通过命令进行排查

```shell
# 查看磁盘空间
df -lh

# 查看内存使用
free -lh

# 查看服务状态和日志
docker logs kong-elasticsearch | kong-logstash | kong-kibana
```

#### Logstash 无法输出到 Elasticsearch？

检查 Logstash 的 pipeline 配置文件中 Elasticsearch 账号密码是否正确
