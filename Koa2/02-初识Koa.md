### Koa是什么

> Koa是基于 Node.js 的下一代 Web 框架

基于 Node.js：它是 Node.js 的模块

下一代：在 Express之后出现的

Web框架：不是命令行工具，不是算法，而是用于 Web 开发

--------------------

### Koa特点

由 Express 原班人马打造

使用 async/await，抛弃回调函数

增强错误处理：try...catch

没有捆绑任何中间件

更小、更富表现力、更健壮

----------------------------------------------------

### Koa初体验

##### 初始化项目

```
npm init
```

##### 安装 Koa

```
npm i koa --save
yarn add koa
```

##### Hello World

```js
// 引入 Koa 库
const Koa = require("koa");
// 创建 Koa 应用
const app = new Koa();
// 注册中间件
app.use((ctx,next) => {
  ctx.body = "Hello World";
})
// 监听端口
app.listen(3000);
```

-------------------------------------

### 自动重启

#### 安装 nodemon

```
npm i nodemon --save-dev
```

#### 使用 nodemon

```
nodemon index.js
```

