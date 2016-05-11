# 前端约定

以下是强制性约定，必须遵守*（特别标注的除外）*

## 文件和目录

  - 由小写字母、数字、下划线_组成

## 缩进

  - 使用4个空格做为一层缩进，请自行配置IDE把一个tab转成4个空格
  - `<html>`, `<head>`, `<body>`, `<script>`的直接后代不缩进

## css

  - 请编辑less文件，保存后会自动编译成css文件，不用写css3前缀，保存时会自动补全前缀

## js

  - 变量用小骆驼命名，私有变量或者不期望别人使用的变量可以使用下划线开头
  - [建议] 用空行隔开不同的逻辑块，方便阅读
  - 使用AMD规范的项目，约定模块名就是文件名，也就说js文件可以放到不同的目录里，但不能重名；
  加载依赖时，约定模板路径就是文件名，示例：

  ```js
  require('search_result')
  ```

  而不是

  ```js
  require('path/to/search_result')
  ```

  碰到这种情况，请配置`js/config.js`的`path`字段
  -  [基于require.js的模块管理](https://github.com/holyzfy/frontend_guidelines/issues/1)
  - jQuery变量请用`$`开头，例如
  
  ```js
  var $submit = $('#login_submit');
  ```


## 注释
    
  - 请删除注释掉的代码，如果有必要保留，请注释说明

## 模拟数据

  - 用有意义的内容填充数据，看起来要像真实的页面
