### 代理对象简介
代理对象就是给一个对象加一层封装，用户访问对象时，不能直接访问对象，而是要访问这层封装来间接访问对象

从而可以通过对封装层进行一些限制，从而限制用户对对象的访问

-----------------------------------------------------

### 创建代理对象
```js
let monitor = new Proxy(需要被代理的对象, 代理限制描述对象);
```
-------------------------------------------------------------------

### 代理限制描述对象

代理对象属性的读取**【查】**
```js
// target就是被代理的对象
// key就是属性名
get(target, key) {}
```

代理对象属性的设置**【增改】**
```js
// target就是被代理的对象
// key就是属性名
// value就是要设置的值
set(target, key, value) {}
```

代理 key in object 操作**【查】**
```js
// target就是被代理的对象
// key就是属性名
has(target, key) {}
```

代理删除对象属性**【删】**
```js
// target就是被代理的对象
// key就是属性名
deleteProperty(target, key) {}
```

代理遍历操作
```js
// target就是被代理对象
ownKeys(target) {}
```

---------------------------------------------

### 代理对象使用例子

```js
let obj = { // 供应商，原始数据
  time: '2017-03-11',
  name: 'net',
  _r: 123
};

let monitor = new Proxy(obj, {
  // 代理对象属性的读取
  get(target, key) {
    return target[key].replace('2017', '2018');
  }

  // 代理对象属性的设置
  set(target, key, value) {
    if (key === 'name') {
      return target[key] = value;
    } else {
      return target[key];
    }
  }

  // 拦截 key in object 操作
  has(target, key) {
    if (key === 'name') {
      return true;
    } else {
      return false;
    }
  }

  // 拦截 delete
  deleteProperty(target, key) {
    if (key.indexof('_') > -1) {
      delete target[key];
        return true;
      } else {
        return false;
    }
  }

  // 拦截Object.keys, Object.getOwnPropertySymbols, Object.getOwnPropertyNames
  ownKeys(target) {
    return Object.keys(target).filter(item => item != 'time');
  }
});

console.log(monitor.time);
monitor.time = '2019';
monitor.name = 'test';
console.log(monitor.time);
delete monitor.time;
console.log(monitor);
delete monitor._r;
console.log(monitor);
console.log(Object.keys(monitor));
```