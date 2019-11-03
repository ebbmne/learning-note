### Reflect简介
Reflect的API与Proxy完全一样

与Proxy区别是：Reflect的是静态方法

### 使用例子
```js
let obj = { // 供应商，原始数据
  time: "2017-03-11",
  name: "net",
  _r: 123
};

console.log(Reflect.get(obj, "time"));
Reflect.set(obj,"name","test");
console.log(Reflect.get(obj, "name");
console.log(Reflect.has(obj, "_r");
```