# Vue组件

## 约定

## 文件目录

Vue组件请做成单独的js文件，按功能放到`js/components`目录或者相应的子目录里，
如果需要用到html模板文件，请把模板文件放到`templates`目录，
建议js文件与模板文件同名

## 代码结构

```js
var options = {
    name: 'my-component', // 建议给组件命名，方便出错时调试
    template: 'templates/my-component.html',
    data: function () {
        return {
            // ...
        };
    },
    components: {
        avatar: components.getAvatar // 组件可以有自己的子组件
    },
    methods: {
        demoOne: function () {},
        demoTwo: function () {
            // 如果方法体有很多行，建议独立成函数
            demoTwo(this);
        }
    }
};

/*
 * @param context 约定第一个参数是Vue的`this`
 */
function demoTwo(context) {
    // ...
}

// ...
```
