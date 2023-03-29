# java 打包 jar

## maven 打包命令

```bash
mvn clean package -DskipTests
```

## java运行命令

```bash
java -Xms512m -Xmx512m -XX:MaxPermSize=256m -jar xxx.jar --server.port=xxxx
```

## IDEA 打包

1. **打开Maven Projects**

2. **选择Lifecycle package**

3. **点击 Toggle "Skip Tests" Mode，禁用 test**

4. **clean**

5. **package**

## IDEA 远程调试

1. **开启远程服务端的调试模式**

    ```bash
    java -jar -Xmx256m -Xms256m -Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=80 /usr/local/jar/xxx.jar
    ```

2. **配置本地的远程调试**

    ```
    1. Run -> Edit Configurations

    2. 添加一个新配置，选择Remote

    3. 配置远程服务地址和端口，端口一定要跟远程服务端命令行里的 address 相同

    4. 启动调试

    address指定调试端口，根据实际环境修改。
    ```

## IDEA 打包时配置 ```-am -amd```

1. 右键 maven 项目列表里的某个模块
2. 打开 ```Lifecycle -> package```，右键 package
3. 在弹出的窗口里配置 Run 选项，点击输入框的 ```Insert Maven Commands...```，选择 ```Maven Option``` 列表里的 ```--also-make```、```--also-make-dependents```，最后点击 ```Insert```
4. 点击 ```Apply``` 和 ```OK```
