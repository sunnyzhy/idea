# 升级 jdk17

## 安装 jdk17

## 配置 jdk17

1. 修改项目的 ```pom.xml```
   ```xml
   <plugins>
      <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <configuration>
              <source>17</source>
              <target>17</target>
          </configuration>
      </plugin>
   </plugins>
   ```
2. 打开 ```File -> Project Structure```
   - 修改 ```Project -> SDK``` 为 ```17```
   - 修改 ```Modules -> Language level``` 为 ```Project default(17)```
3. 打开 ```File -> Settings -> Build,Execution,Deployment -> Compiler -> Java Compiler```
   - 修改 ```Project bytecode version``` 为 ```17```
   - 修改 ```Per-module bytecode version``` 列表里的 ```Target bytecode version``` 为 ```17```

***此流程适用于升级其他 jdk 版本。***
