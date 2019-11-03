### Decorator简介
Decorator是装饰器，装饰器是一个**函数**，该函数用**增强类**的功能

-----------------------------------

### Decorator定义

```js
function(target, name, descriptor) {}
```

| 参数       | 说明             |
| ---------- | ---------------- |
| target     | 代表装饰的类     |
| name       | 代表装饰的属性名 |
| descriptor | 属性描述符       |

----------------------------------------------------

### 属性描述符

| 属性         | 说明                         | 可选值     | 默认值    |
| ------------ | ---------------------------- | ---------- | --------- |
| writable     | 是否可写                     | true/false | false     |
| configurable | 是否可以被删除或再次进行修改 | true/false | false     |
| enumerable   | 是否可枚举                   | true/false | false     |
| value        | 被描述属性的值               | 任意类型   | undefined |

-----------------------------------------------------------------------------------------

### Decorator使用

在需要被修饰的类或类的属性上使用`@修饰器名(参数列表)`即可

-----------------------------------------------

### Decorator例子

#### 只读装饰器

```js
let readonly = function(target, name, descriptor) {
  descriptor.writeable = false;
  return descriptor;
};

class Test {
  @readonly
  time() {
    return "2017-03-11"
  }
}

let test = new Test();
  
// 下面的代码会报错
test.time = function() {
  console.log("reset time");
}
```

#### 给类加静态属性

```js
let typename = function(target, name, descriptor) {
  target.myname = "hello";
}

@typename
class Test {}

console.log(Test.myname);
```

#### 日志功能

```js
let log = (type) => {
  return function(target, name, descriptor) {
    let src_method = descriptor.value;
    descriptor.value = (...arg) => {
      src_method.apply(target, arg);
        console.info(`log ${type}`);
    }
  }
}
  
class AD {
  @log("show")
  show() {
    console.info("ad is show");
  }

  @log("click")  
  click() {
    console.info("ad is click");
  }
}

let ad = new AD();
ad.show();
ad.click();
```