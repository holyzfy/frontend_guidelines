# 前端约定

以下是强制性约定，必须遵守 *（特别标注的除外）*

## 文件和目录

由小写字母、数字、下划线_组成 *（引用的第三方文件除外）*

## 缩进

- 使用4个空格做为一层缩进，请自行配置编辑器把一个tab转成4个空格
- `<html>`, `<head>`, `<body>`, `<script>`, `<style>`的直接后代不缩进

## css

请配置编辑器，要求能把less或者scss文件编译成同名的css文件，并自动加上css3前缀，例如[给Sublime Text 3配置SASS](https://github.com/holyzfy/frontend_guidelines/issues/4)

## js

- 写字符串时优先使用单引号
- 变量用小骆驼命名，私有变量或者不期望别人使用的变量可以使用下划线开头
- [建议] 用空行隔开不同的逻辑块，方便阅读
-  [基于require.js的模块管理](https://github.com/holyzfy/frontend_guidelines/issues/1)
- jQuery变量请用`$`开头，例如

    ```js
    var $submit = $('#login_submit');
    ```

## ajax

```js
{
    "data": {
        // 数据
    },
    "message": "请求成功", // 描述
    "status": 0 // 0表示成功，其他整数表示失败
}
```

## 注释
    
请删除注释掉的代码，如果有必要保留，请注释说明

## 模拟数据

用有意义的内容填充数据，看起来要像真实的页面
