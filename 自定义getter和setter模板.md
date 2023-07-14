# 自定义 getter 和 setter 模板

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
