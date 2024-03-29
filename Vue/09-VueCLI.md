### Vue CLI 介绍

CLI：Command-Line Interface，翻译为命令行界面，俗称脚手架

Vue CLI 是一个用于搭建出Vue开发环境的工具，它能够配置好webpack以及代码目录结构、项目构建、项目部署、热加载、代码单元测试等事情

### Vue CLI 安装

```shell
npm install -g @vue/cli
```

### Vue CLI 版本

Vue CLI 分为两个版本，分别为 Vue CLI 2 和 Vue CLI 3

| Vue CLI 2                         | Vue CLI 3                       |
| --------------------------------- | ------------------------------- |
| 基于 Webpack3，编译打包速度比较慢 | 基于 Webpack4，编译打包速度更快 |
| 不隐藏配置文件，工程目录繁杂      | 隐藏配置文件，工程目录清晰简洁  |
| 只能通过命令行进行操作            | 提供可视化配置工具              |
| 不支持TypeScript和PWA             | 支持TypeScript和PWA             |

 下载的`@vue/cli` 是 Vue CLI 3版本，但是 Vue CLI 3版本只要装上一个桥接工具后也可以使用 Vue CLI 2 的功能

```shell
npm install -g @vue/cli-init
```

### Vue CLI 使用

创建 Vue CLI 2 风格的项目工程

```shell
vue init webpack [项目名称]
```

生成的目录结构

![](./image/vuecli2.png)

创建 Vue CLI 3 风格的项目工程

```shell
vue create [项目名称]
```

生成的目录结构

![](./image/vuecli3.png)

启动可视化配置工具

```shell
vue ui
```

进行组件原型开发

```html
<!-- App.vue -->
<template>
    <h1>{{ welcome }}</h1>
</template>

<script>
export default {
    data() {
        return {
            welcome: "Hello Vue-cli 3.0"
        }
    }
}
</script>
```
```shell
# App.vue 所在目录
vue serve
```

### runtime-only和runtime-compiler

#### Vue程序运行过程

​    模板字符串经过解析得到抽象语法树 ==> 

​    抽象语法树经过编译为render函数表示 ==> 

​    执行render函数生成虚拟dom ==> 

​    用虚拟dom创建出真实dom

![](./image/vue-runtime.png)

#### runtime-compiler

将 `模板字符串 ==> ast ==> render函数` 这些步骤交给客户端来做，即工程编译打包后的文件中包含编译器代码和模板字符串代码

生成的代码

```js
new Vue({
    el: "#app",
    components: { App },
    template: `<App/>`
});
```

#### runtime-only

将 `模板字符串 ==> ast ==> render函数` 这些步骤在Webpack打包时进行，即工程编译打包后的文件中不包含编译器代码、不包含模板字符串代码，包含已成生成了的render函数

生成的代码

```js
new Vue({
    render: h => h(App);
}).$mount("#app");

// $mount的作用与el相同，写了el，在底层也会调用$mount函数，即等价于下面的写法

new Vue({
    el: "#app",
    render: h => h(App);
});
```

#### 两种模式选择

runtime-only比起runtime-compiler更好，体现在

* 打包体积更少（不用带解析器和编译器代码和模板字符串代码）
* 运行速度更快（客户端不用进行解析和编译）

#### render函数了解

render中的 h 是一个形参的名字，实际传入的是 Vue 的 `createElement`函数

`createElement`函数的使用

```js
createElement('标签名', '相关数据对象', ['内容数组']);
```

例子

```js
new Vue({
    el: "#app",
    render: (createElement) => {
        return createElement("div", {class: "box"}, [
            "MyComponent", "", createElement(
                "h2", "", ["这里是标题"]
            );
        ])
    }
});
```

<br/>

### devtools

`devtools`是`Vue`官方推出一个调试工具，可以通过谷歌浏览器插件的形式进行安装，如果不能访问谷歌浏览器商店，则可以通过下面的方式进行下载、安装和使用

#### 下载与安装

```shell
# 通过npm安装
$ npm install -g @vue/devtools
# 通过yarn安装
$ yarn global add @vue/devtools
```

#### 使用

```shell
$ vue-devtools
```

