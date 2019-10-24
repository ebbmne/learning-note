### Web路由发展阶段

#### 阶段一：后端渲染阶段

|      | 说明                                                         |
| ---- | ------------------------------------------------------------ |
| 概念 | 用户在浏览器输入特定的URL，浏览器发送请求到服务器<br/>服务器接收请求，使用正则分析URL后，判断用户想要获取什么样的资源<br/>服务器使用`jsp`、`php`等模板引擎，生成好HTML或数据，即渲染好页面后返回给前端进行显示 |
| 优点 | 利于搜索引擎SEO                                              |
| 缺点 | HTML代码和数据以及对应的逻辑会混在一起,                      |

#### 阶段二：前后端分离阶段

|      | 说明                                                         |
| ---- | ------------------------------------------------------------ |
| 概念 | 前端负责使用JS进行页面的渲染，后端只提供API来返回数据，前端通过Ajax获取数据 |
| 优点 | 前后端责任的清晰, 后端专注于数据上, 前端专注于交互和可视化上<br/>当需要移动端时，后端不需要进行任何处理，依然使用之前的一套API即可 |
| 缺点 | 不利于搜索引擎SEO                                            |

#### 阶段三：单页面应用阶段

|      | 说明                                                         |
| ---- | ------------------------------------------------------------ |
| 概念 | SPA与前后端分离类似<br/>区别是由前端进行路由的管理，路由改变时，服务器返回相同的文件，但页面不刷新而是加载不同的组件 |
| 优点 | 组件按照路由进行加载，避免页面的刷新                         |
| 缺点 | 不利于搜索引擎SEO<br/>需要后端做特殊配置，对于任何URL都返回同一个HTML |

<br/>

### 实现前端路由的方式

前端路由的核心需求在于路由改变，但是页面不刷新，有两种方法能实现这种需求

#### 方式一：使用URL的hash

概念：URL的hash也就是锚点(#)

本质：本质上是改变window.location的href属性

优点：兼容性好

缺点：URL不好看，URL中必然会有`/#/`

#### 方式二：使用HTML5的history对象

概念：history对象是HTML5新增，它可以实现改变页面URL却不刷新页面

本质：history对象本质上是一个栈结构，URL始终是栈顶的路径

API：一共有5个

| API                                        | 说明                                                         |
| ------------------------------------------ | ------------------------------------------------------------ |
| history.pushState(state, title, "路径")    | state：一个对象，用于存储历史记录的相关信息<br/>title：简短的标题来表示state<br>将路径推入栈，后退按钮可以显示，即保留历史记录 |
| history.replaceState(state, title, "路径") | 类似于pushState<br/>区别是栈顶元素替换为路径，但不保留历史记录，即不能前进后退 |
| history.go(n)                              | n是一个整数，表示前进/后退n个路由<br/>当n>0时前进，当n<0时后退 |
| history.back()                             | 后退一个路由，相当于history.go(-1)                           |
| history.forward()                          | 前进一个路由，相当于history.go(1)                            |

优点：URL好看，URL中不需要带有`/#/`

缺点：兼容性不是很好，需要浏览器支持HTML5

<br/>

### 初识vue-router

#### 简介

vue-router是Vue.js官方的路由插件，适合用于构建单页面应用

在vue-router的单页面应用中，页面的路径的改变就是组件的切换

#### 下载与安装

使用npm进行安装

```shell
npm install vue-router --save
```
使用yarn进行安装
```shell
yarn add vue-router
```

<br/>

### 路由器对象

#### 1. 创建路由器对象

属性选项

| 属性选项        | 说明                                                         | 是否可选 |
| --------------- | ------------------------------------------------------------ | -------- |
| routes          | 路由数组                                                     | 必填     |
| mode            | 用于定义路由模式<br/>history：HTML5的history模式<br/>hash：URL的hash模式（默认） | 可选     |
| linkActiveClass | 自定义选中时的class名字                                      | 可选     |

例子

```js
/* src/router/index.js */

import Vue from "vue";
import VueRouter from "vue-router";

// 1. 注入插件
Vue.use(VueRouter);

// 2. 定义路由数组
const routes = [];

// 3. 创建路由对象
const router = new VueRouter({
    mode: "history", // 使用history模式
    linkActiveClass: "active", // 自定义选中的class名字
    routes
});

// 4. 导出路由对象
export default router;
```

#### 2.定义路由

每个路由是一个对象，其属性如下

| 属性      | 说明                                     |
| --------- | ---------------------------------------- |
| name      | 路由的名字                               |
| path      | 匹配的路径                               |
| component | 组件对象                                 |
| children  | 嵌套路由数组，每个元素是一个嵌套路由对象 |

所有的路由放在路由数组中

```js
const routes = [
  {
    name: "路由1",
    path: "匹配的路径1", 
    component: 组件对象1
  },
  {
    name: "路由2",
    path: "匹配的路径2", 
    component: 组件对象2,
    children: [
      嵌套路由对象,
      嵌套路由对象,
      嵌套路由对象
    ]
  },
  {
    name: "路由3",
    path: "匹配的路径3", 
    component: 组件对象3
  }
];
```

设置默认路径

```js
{
  name: "默认路由",
  path: "/",
  component: 默认组件对象
}
```

例子

```js
const routes = [
  {
    name: "root",
    path: "/",
    component: Home
  }
  {
    name: "home",
    path: "/home", 
    component: Home,
    children: [
      {
        name: "message",
        path: "/message", // 匹配 /home/message
        component: HomeMessage
      },
      {
        name: "news",
        path: "/news", // 匹配 /home/news
        component: HomeNews
      }
    ]
  },
  {
    name: "about",
    path: "/about", 
    component: About
  },
  {
    name: "music",
    path: "/music", 
    component: Music
  }
];
```

#### 3.将路由器对象挂载到Vue根实例中

```js
// main.js
import Vue from "vue";
import App from "src/App.vue";
import router from "src/router";

new Vue({
  el: "#app",
  render: h => h(App),
  router,
});
```

<br/>

### 路由跳转

#### 方式一：通过路由组件

##### router-link组件

`router-link`组件是一个`vue-router`中已经内置的组件，用于设置跳转链接

`router-link`属性选项

| 属性选项           | 说明                                                         | 是否必填 |
| ------------------ | ------------------------------------------------------------ | -------- |
| to                 | 一个对象或字符串<br/>path：指定跳转的路径<br/>query：query参数对象（可选） | 必填     |
| tag                | 指定\<router-link>之后渲染成什么组件，默认是`a标签`          | 选填     |
| replace            | replace不会留下history记录<br/>即使用replace时，后退键返回不能返回到上一个页面中 | 选填     |
| active-class       | 路由匹配成功时，会自动给当前元素设置一个`router-link-active`的class<br/>`router-link-active`是默认的名字，可以在路由对象定义处进行自定义 | 选填     |
| exact-active-class | 类似于`active-class`，区别是只在精准匹配下才会添加class      | 选填     |

##### router-view组件

`router-view`组件是一个`vue-router`中已经内置的组件，用于根据选定路由动态渲染出不同的组件，即起到占位的作用

`router-view`与`router-link`放在一起，搭配使用

##### 例子

```vue
<template>
    <div>
        <h1>我是网站标题</h1>
        <router-link to="/home">首页</router-link>
        <router-link 
          :to="{
            path: '/about',
            query: {name: 'js', age: 20}
          }">关于</router-link>
        <router-view></router-view>
    </div>
</template>
```

#### 方式二：通过路由器对象

所有Vue实例/组件中都有`$router`属性，通过该属性可以访问到路由器对象

使用路由器对象的`push`、`replace`、`go`、`back`和`forward`方法进行路由跳转

```js
export default {
  name: "App",
  methods: {
    linkToHome() {
      this.$router.push("/home");
    },
    linkToAbout() {
      this.$router.replace("/about");
    }
  }
}
```

<br/>

### 路由传参

路由传参有动态路由和query参数两种方案

#### 方式一：动态路由

对于路由的定义：动态值前加上`:`

```js
{
  path: "/user/:id",
  component: User
}
```

对于路由地址的定义：写具体的动态值

```vue
<router-link to="/user/123">用户</router-link>
```

```js
this.$router.push("/user/123");
```

获取动态值：使用`$route`获取当前URL对象，通过`$route.params`获取当前URL对象的动态值

```js
this.$route.params.id
```

#### 方式二：query参数

对于路由的定义：不需要改动，因为用到的是URL本身支持的query参数

```js
{
  path: "/user",
  component: User
}
```

对于路由地址的定义：写具体的参数值

```vue
<router-link 
  :to="{
    path: '/user',
    query: {id:123}
  }">用户
</router-link>
```

获取参数

```js
let params = this.$route.query.split("&");
let obj = {};
params.forEach(function(item) {
  let keyAndValue = item.split("=");
  obj[keyAndValue[0]] = keyAndValue[1];
});
```

<br/>

### 路由懒加载

#### 路由懒加载的需求

当打包构建应用时，JavaScript包会变得非常大，影响页面加载，甚至用户的电脑上还出现了短暂空白的情况

如果我们能把不同路由对应的组件分割成不同的代码块，然后当路由被访问的时候才加载对应组件的代码，这样就更加高效

#### 路由懒加载的作用

路由懒加载的主要作用就是将路由对应的组件打包成一个个的js代码块放在不同的js文件中

只有在这个路由被访问到的时候, 才加载对应的js文件及其组件

#### 路由懒加载的实现

1. Vue的异步组件和Webpack的代码分析

   ```js
   const Home = resolve => { require.ensure(['../components/Home.vue'], () => { resolve(require('../components/Home.vue')) })};
   ```

2. AMD写法

   ```js
   const About = resolve => require(['../components/About.vue'], resolve);
   ```

3. ES6 Module写法

   ```js
   const Home = () => import("../components/Home.vue");
   ```

<br/>

### 导航守卫

导航守卫可以理解为路由的钩子函数，在路由切换时触发

#### 导航守卫的回调函数

```js
(to, from, next) => {}
```

| 参数 | 说明                                                         |
| ---- | ------------------------------------------------------------ |
| to   | 即将要进入的路由对象，即routes数组里面配置的某个具体的路由对象 |
| from | 即将离开的路由对象，即routes数组里面配置的某个具体的路由对象 |
| next | 一定要调用next方法来**resolve**钩子，否则无法进行跳转<br/>next()：按规则进行路由跳转<br/>next(false)：阻止页面跳转<br/>next({ path: "/", query: {}})：跳转到其他的路由<br/>next(error)：导航会被终止且该错误会被传递给 `router.onError()`注册过的回调 |

#### 导航守卫分类

| 分类         | 特点                         |
| ------------ | ---------------------------- |
| 全局守卫     | 在router定义时设置           |
| 路由独享守卫 | 在route定义时设置            |
| 组件内守卫   | 在使用`路由组件`的组件中设置 |

#### 全局守卫

| 概念         | 说明                                       |
| ------------ | ------------------------------------------ |
| 作用         | 监测所有的路由                             |
| 书写位置     | 写在路由器定义页面                         |
| 全局前置守卫 | router.beforeEach((to, from, next)=>{})    |
| 全局解析守卫 | router.beforeResolve((to, from, next)=>{}) |
| 全局后置钩子 | router.afterEach((to, from)=>{})           |

`router.afterEach`中不接受也不能使用`next`函数

#### 路由独享守卫

| 概念           | 说明                                |
| -------------- | ----------------------------------- |
| 作用           | 监测某个特定的路由                  |
| 书写位置       | 写在具体路由对象里面                |
| 路由独享的守卫 | beforeEnter: (to, from, next) => {} |

#### 路由组件守卫

| 概念      | 说明                                  | 注意事项                                                     |
| --------- | ------------------------------------- | ------------------------------------------------------------ |
| 作用      | 监测该组件中的所使用到的所有路由组件  |                                                              |
| 书写位置  | 组件的参数中                          |                                                              |
| 钩子方法1 | beforeRouteEnter (to, from, next) {}  | 不能获取组件实例 `this`<br/>因为此时组件实例还没被创建       |
| 钩子方法2 | beforeRouteUpdate (to, from, next) {} | 在当前路由改变，但是该组件被复用时调用<br/>可以访问组件实例 `this` |
| 钩子方法3 | beforeRouteLeave (to, from, next) {}  | 可以访问组件实例 `this`                                      |

`beforeRouteEnter`不能获取组件实例 `this`，因为此时组件实例还没被创建，但可以通过传一个回调给 `next`来访问组件实例

```js
beforeRouteEnter (to, from, next) {
  next(vm => {
    // 通过 `vm` 访问组件实例
  })
}
```

 对于 `beforeRouteUpdate` 和 `beforeRouteLeave` 来说，`this` 已经可用了，所以**不支持**传递回调，因为没有必要了 

