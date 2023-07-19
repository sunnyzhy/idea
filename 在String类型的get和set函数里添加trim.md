# 在 ```String``` 类型的 ```get/set``` 函数里添加 ```trim```

## 自定义 getter 和 setter 模板

***对 ```String``` 类型的字符串进行 ```trim()``` 处理。***

1. 按下 ```alt + insert``` 快捷键选择 ```Getter and Setter```
2. 点击 ```Getter template``` 模板后面的 ```...```， 创建自定义的 ```Getter``` 模板：
    ```java
    #if($field.modifierStatic)
    static ##
    #end
    $field.type ##
    #if($field.recordComponent)
      ${field.name}##
    #else
    #set($name = $StringUtil.capitalizeWithJavaBeanConvention($StringUtil.sanitizeJavaIdentifier($helper.getPropertyName($field, $project))))
    #if ($field.boolean && $field.primitive)
      is##
    #else
      get##
    #end
    ${name}##
    #end
    () {
      #if($field.string)
        return $field.name == null ? null : $field.name.##
      trim();
      #else
        return $field.name;
      #end
    }
    ```
3. 点击 ```Setter template``` 模板后面的 ```...```， 创建自定义的 ```Setter``` 模板：
    ```java
    #set($paramName = $helper.getParamName($field, $project))
    #if($field.modifierStatic)
    static ##
    #end
    void set$StringUtil.capitalizeWithJavaBeanConvention($StringUtil.sanitizeJavaIdentifier($helper.getPropertyName($field, $project)))($field.type $paramName) {
      #if ($field.name == $paramName)
        #if (!$field.modifierStatic)
          this.##
        #else
          $classname.##
        #end
      #end
      $field.name = ##
      #if($field.string)
        $paramName == null ? null : $paramName.##
    trim();
      #else
        $paramName;
      #end
    }
    ```
4. 生成的 ```get/set``` 示例：
    ```java
    private String text;
    
    public String getText() {
        return text == null ? null : text.trim();
    }
    
    public void setText(String text) {
        this.text = text == null ? null : text.trim();
    }
    ```

## 反射

```java
@Test
void ref() throws IllegalAccessException, NoSuchFieldException {
    trim(" aa bb  ");
}

void trim(String s) throws IllegalAccessException, NoSuchFieldException {
    System.out.println(s);
    Class cls = s.getClass();
    Field field = cls.getDeclaredField("value");
    if (field != null) {
        field.setAccessible(true);
        field.set(s, s.trim().toCharArray());
    }
    System.out.println(s);
}
```

## 使用 ```@AutoTrim``` 注解

github 网址：```https://github.com/supalle/auto-trim.git```

***仅支持 ：```java.lang.String：``` 类型的变量进行 ：```AutoTrim：``` 操作。***

1. 添加依赖
    ```xml
    <dependency>
        <groupId>com.supalle</groupId>
        <artifactId>auto-trim</artifactId>
        <version>1.0.0</version>
        <scope>provided</scope>
    </dependency>
    ```
2. ```@AutoTrim``` 注解可以作用于：
   - ```ElementType.TYPE```：class类、接口
   - ```ElementType.CONSTRUCTOR```：构造函数
   - ```ElementType.FIELD```：属性
   - ```ElementType.METHOD```：方法
   - ```ElementType.PARAMETER```：方法形参

## Mybatis

```java
@Target({ElementType.FIELD})
@Retention(RetentionPolicy.RUNTIME)
public @interface Trim {
}

@Intercepts(@Signature(type = Executor.class, method = "update", args = {MappedStatement.class, Object.class}))
public class TrimInterceptor implements Interceptor {
    @Override
    public Object intercept(Invocation invocation) throws Throwable {
        Object arg = invocation.getArgs()[1];
        Class cls = arg.getClass();
        Field[] fields = cls.getDeclaredFields();
        for (Field field : fields) {
            if (field.getType() == String.class) {
                Trim trim = field.getAnnotation(Trim.class);
                if (trim != null) {
                    PropertyDescriptor pd = new PropertyDescriptor(field.getName(), cls);
                    Method readMethod = pd.getReadMethod();
                    if (readMethod != null) {
                        Object value = readMethod.invoke(arg);
                        if (value != null) {
                            Method writeMethod = pd.getWriteMethod();
                            writeMethod.invoke(arg, value.toString().trim());
                        }
                    }
                }
            }
        }
        return invocation.proceed();
    }

    @Override
    public Object plugin(Object o) {
        return Plugin.wrap(o, this);
    }

    @Override
    public void setProperties(Properties properties) {
        System.out.println(properties);
    }
}

@Configuration
public class InterceptorConfig {
    @Bean
    public Interceptor[] interceptors(){
        TrimInterceptor trimInterceptor = new TrimInterceptor();
        return new Interceptor[]{trimInterceptor};
    }
}

public class TrimPlugin extends PluginAdapter {
    private String annotation = "@Trim";
    private String importedType;
    private FullyQualifiedJavaType javaType;

    public TrimPlugin() {
        importedType = "com.zhy.annotation.Trim";
        javaType = new FullyQualifiedJavaType(importedType);
    }

    @Override
    public boolean modelFieldGenerated(Field field, TopLevelClass topLevelClass, IntrospectedColumn introspectedColumn, IntrospectedTable introspectedTable, ModelClassType modelClassType) {
        List<IntrospectedColumn> pkcs = introspectedTable.getPrimaryKeyColumns();
        if (("CHAR".equals(introspectedColumn.getJdbcTypeName()) || "VARCHAR".equals(introspectedColumn.getJdbcTypeName())) && pkcs.indexOf(introspectedColumn) < 0 && introspectedColumn.getLength() > 0) {
            if (!topLevelClass.getImportedTypes().contains(javaType)) {
                topLevelClass.addImportedType(importedType);
            }
            field.addAnnotation(annotation);
        }
        return true;
    }

    @Override
    public boolean validate(List<String> warnings) {
        return true;
    }
}
```

最后在 ```generatorConfig.xml``` 里添加插件：

```xml
<plugin type="com.zhy.plugin.TrimPlugin" />
```
