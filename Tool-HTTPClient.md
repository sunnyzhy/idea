# Tool - HTTPClient

## 上传文件

controller:

```java
@PostMapping(value = {"/upload"})
public boolean upload(@RequestParam MultipartFile file, @RequestParam Map<String, Object> params)
```

HTTP Client Tool:

```
POST http://localhost:8080/upload
Content-Type: multipart/form-data; boundary=WebAppBoundary
token: 2aed1dc9-7507-11ed-93d8-7427ea652c28

--WebAppBoundary
Content-Disposition: form-data; name="groupId"

1
--WebAppBoundary
Content-Disposition: form-data; name="file"; filename="a5cada5f09044eda974782e1dd94ac78.xlsx"

< D:\upload\a5cada5f09044eda974782e1dd94ac78.xlsx
--WebAppBoundary--

###
```

参数说明:

- ```Content-Type: multipart/form-data;```: 如果是上传文件，就必须包含此请求头
- ```boundary=WebAppBoundary```: 定义 ```form-data``` 各个参数之间的分隔边界符，此处为 ```WebAppBoundary```
- ```token: 2aed1dc9-7507-11ed-93d8-7427ea652c28```: 自定义 ```http``` 请求头的上下文参数
- ```--WebAppBoundary```: ```--``` + 上文定义的分隔边界符 ```WebAppBoundary```，注意：
   - ***分隔边界符的前面必须是两个英文符号的短横线 ```--```***
   - *** ```--WebAppBoundary``` 下面定义参数的名称和值，名称和值之间有一行空白行***
   - ***参数列表以 ```--WebAppBoundary--``` 结尾***
- ```form-data``` 参数对应 ```controller``` 接口的参数列表
- ```groupId```: ```form-data``` 参数
   
   ```
   --WebAppBoundary
   Content-Disposition: form-data; name="groupId"
   
   1
   ```
   
   注意:

   - 上下文中间有一行空白行
   - ```groupId``` 是 ```controller``` 接口参数 ```Map<String, Object> params``` 里的自定义参数之一
   - ```file```: ```form-data``` 参数，定义上传的文件
   
      ```
      --WebAppBoundary
      Content-Disposition: form-data; name="file"; filename="a5cada5f09044eda974782e1dd94ac78.xlsx"
         
      < D:\upload\a5cada5f09044eda974782e1dd94ac78.xlsx
      ```
   
      注意:
   
      - ```--WebAppBoundary``` 为参数定义的起始位置
      - ```name="file"``` 对应 ```controller``` 接口参数 ```MultipartFile file```，可以取其他的名称，但是一一必须对应
      - ```filename``` 为上传的文件名
      - 空白行
      - 具体的文件路径
