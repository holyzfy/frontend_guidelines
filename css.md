# css

- [css属性书写顺序](#css属性书写顺序)
- [class命名](#class命名)

## css属性书写顺序

选择器效率，浏览器渲染过程，重绘(repaint)，重排(reflow)

0. 显示属性

  - display 
  - list-style 
  - position 
  - float 
  - clear 

0. 盒子模型

  - width 
  - height 
  - margin 
  - padding 
  - border 
  - background 

0. 文本属性

  - color 
  - font 
  - text-decoration 
  - text-align 
  - vertical-align 
  - white-space 
  - other text 
  - content

## class命名

- 类名按功能来命名，比如.highlight，尽量不要这么写.red，比如效果图里把红色改成了黄色，那.red就不太合适了

- css属性backgroud, border之类的尽量用缩写形式 

- 选择器不要用id，把id留给脚本用

- 简化CSS选择器：控制选择器的深度，越短越好，示例：

  坏的写法:
  
  ```css
  .tree  .tree-item {...}
  div.box  div  div  .item {...}
  .box  * {...}
  ```
  
  
  好的写法:
  
  ```css
  .tree-item {...}
  .box  .item {...} /*把*替换成具体的标签或类名*/
  ```

- 复用

  从外观相似的容器里抽象出共用的样式，示例：

  ```html
  <div class="box help">
       <h2 class="box-hd">标题</h2>
       <div class="box-bd help-bd">内容 。。。</div>
       <div class="box-ft">尾部</div>
  </div>
  ```
  
  .box是通用的样式类名，只写最基本的外观样式，.help具体的功能类名，
  如果要覆盖.box-bd里的某个样式可以用.help .box-bd{}来覆盖，也可以用.help-bd来覆盖
  
- 常用类名

  - 页眉  header
  - 页脚  footer
  - 侧边栏 aside
  - 大导航 nav
  - 面包屑导航 crumb
  - 图文混杂在一起的容器  figure
  - 输入框 field
  - 放置一些链接的容器 tools
  - 列表  list
  - 选项卡 tab
  - 提示  tip
  - 按钮  btn + 表达功能的单词，例如:btn-login, btn-search, btn-buy
  - 对于大块容器，实在想不出起什么名字，可以从这里选一个：box, section, content, grid
  
  一个典型的容器可以拆分为三部分：头部（`*-hd`），中部（`*-bd`），尾部（`*-ft`），结构如下：

  ```html
  <div class="help">
       <h2 class="help-hd">标题</h2>
       <div class="help-bd">内容 。。。</div>
       <div class="help-ft">尾部</div>
  </div>
  ```
  
