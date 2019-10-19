### Vue介绍

Vue是一套用于构建用户界面的渐进式框架，便于与第三方库或既有项目整合

Vue框架只关注视图层，负责处理View层和Model层的联系

Vue的技术栈组成：Vue + Vue-Router + Vuex

<br/>

### Vue特点

* 渐进式框架，便于与第三方库或既有项目整合
* 单向数据流，子组件不能直接修改父组件传递过来的数据
* 组件化开发，可实现代码的复用
* 声明式编程，不用写dom操作代码
* 虚拟dom，加快页面渲染速度

<br/>

### Vue安装

通过Script标签引入本地文件

```html
<script src="./vue.js"></script>
```

通过Script标签引入CDN文件

```html
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

通过npm安装

```shell
npm install vue
```

通过脚手架安装

```shell
npm install -g @vue/cli
vue create [项目名]
```

