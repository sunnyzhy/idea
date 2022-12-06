# Tool - HTTPClient

## 上传文件

controller:

```java
@PostMapping(value = {"/upload"})
public bool upload(@RequestParam MultipartFile file, @RequestParam Map<String, Object> params)
```

HTTP Client Tool:

```http
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

- ```Content-Type: multipart/form-data;```: 上传文件，```http``` 必须包含此请求头
- ```boundary=WebAppBoundary```: 定义 ```form-data``` 各个参数之间的分隔边界符
- ```token: 2aed1dc9-7507-11ed-93d8-7427ea652c28```: 自定义 ```http``` 请求头的上下文参数
- ```--WebAppBoundary```: 是上文定义的分隔边界，```form-data``` 的所有参数均包含在 ```--WebAppBoundary``` 和 ```--WebAppBoundary--``` 之间，其中各参数之间用 ```--WebAppBoundary``` 分隔
- ```form-data``` 参数对应 ```controller``` 接口参数
- ```groupId```: ```form-data``` 参数
   ```
   Content-Disposition: form-data; name="groupId"
   
   1
   ```
   注意:
      - 上下文中间有一行空白行
      - ```groupId``` 是 ```controller``` 接口参数 ```Map<String, Object> params``` 里的自定义参数之一
- ```file```: ```form-data``` 参数，定义上传的文件
   ```
   Content-Disposition: form-data; name="file"; filename="a5cada5f09044eda974782e1dd94ac78.xlsx"
   
   < D:\upload\a5cada5f09044eda974782e1dd94ac78.xlsx
   ```
   注意:
      - 须指定 ```filename``` 和具体的文件路径
      - 上下文中间有一行空白行
      - ```file``` 对应 ```controller``` 接口参数 ```MultipartFile file```，名称必须对应
