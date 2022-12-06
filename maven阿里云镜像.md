# maven 阿里云镜像

maven 阿里云镜像现在使用的是 https 协议，而不再是http。

## 以往的配置 (http)

```xml
<mirror>
   <id>alimaven</id>
   <mirrorOf>central</mirrorOf>
   <name>aliyun maven</name>
   <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
</mirror>
```

## 现在的配置 (https)

[aliyun maven](https://developer.aliyun.com/mirror/maven?spm=a2c6h.13651102.0.0.73d41b111PbK77 'aliyun maven')

1. 修改 .\conf\settings.xml
   ```xml
   <mirror>
       <id>aliyunmaven</id>
       <mirrorOf>*</mirrorOf>
       <name>阿里云公共仓库</name>
       <url>https://maven.aliyun.com/repository/public</url>
   </mirror>
   ```
2. 在 IDEA 中设置忽略 HTTPS 的 SSL 证书验证:
   - 打开 File -> Settings -> Maven -> Importing -> VM options for importer
   - 添加 -Dmaven.wagon.http.ssl.insecure=true -Dmaven.wagon.http.ssl.allowall=true
