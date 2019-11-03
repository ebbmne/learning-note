### Symbol数据类型简介
Symbol类型提供一个全局独一无二的值

Symbol类型是基础数据类型

---------------------------------------------------

### Symbol类型变量声明定义

通过Symbol()函数，因为Symbol是基础类型，所以不能用new操作符
```js
let a = Symbol();
let b = Symbol();
console.log(a === b); // false
```

通过Symbol.for("标识符")
```js
let a = Symbol.for("ES6");
let b = Symbol.for("ES6");
console.log(a === b); // true
```

---------------------------------------------

### Symbol变量的使用

```js
let symbol = Symbol.for('ES6');
let obj = {
  [symbol]: "ECMAScript 6"
}
console.log(obj); // { Symbol(ES6): 123 }
console.log(obj[Symbol.for("ES6")]); // "ECMAScript 6"
```
---------------------------------

### Symbol变量的遍历相关

* 通过 Object.entries 和 for-in 循环是取不到的
* 要用 Object.getOwnPropertySymbol(obj).forEach((item) => {})