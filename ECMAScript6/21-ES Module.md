### 导出模块

> 导出模块有3种方法

#### export default 对象

一个模块中只能有一个 `export default [对象]` 语句

默认导入对象，其他文件导入该模块时，可以自定义这个对象的名字

```js
// 对象是已经声明好的
let a = 10;
export default a;

// 以下代码报错，因为在使用 export default 时不能边声明边导出
export default const b = 20; // error
```

#### export 对象声明语句

一个模块中可以有多个 `export 对象声明语句` 语句
```js
export let a;
export let b;
```

导出的对象在声明时一般进行可以初始化
```js
export let a = 10;
export let b = () => {console.log(20)};
```

其他文件导入该模块时，需要指定导入哪些对象，即名字要一一对应

#### export { 对象1, 对象2, 对象3, ... }

一个模块中可以有多个 `export { 对象1, 对象2, 对象3, ... }` 语句
```js
let a = 10;
let b = () => {console.log(20)};
let c = true;
export { a, b };
export { c };
```

导出的对象必须是已经声明好的，导出时可以使用 `as` 起别名
```js
let a = 10;
let b = () => {console.log(20)};
let c = true;
export { a as A, b };
export { c as C };
```

其他文件导入该模块时，需要指定导入哪些对象，即名字要一一对应

---------------------------------------------

### 导入模块

> 导入模块有两种方式

#### import 自定义名称 from 模块文件路径

这种导入方式导入的是模块的默认导出对象，即对应导入 `export default [对象]` 导出的对象

#### import { 对象名1, ..., 对象名n } from 模块文件路径

这种导入方式导入的是模块指定导出的对象，名字要一一对应，即对应 `export [对象]` 导出的对象

#### 导入时的注意点

##### 可以使用 as 为导入的对象起别名

`import { 对象名1 as 自定义别名, ..., 对象名n } from 模块文件路径`

##### 使用 \* 可以导入模块导出的全部对象

`import * as 自定义别名 from 模块文件路径`

----------------------------------------

### 浏览器引入模块

浏览器要引入ES6 Module的模块文件时，需要指明类型为`module`
```html
<script src="" type="module"></script>
```