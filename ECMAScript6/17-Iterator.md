###  对象迭代器定义方法
给对象添加名为`[Symbol.iterator]`的函数

`[Symbol.iterator]`函数返回一个对象，该对象有名为`next`的函数属性

`next`函数返回一个对象，该对象拥有`value`和`done`两个属性

* value: 本次next返回的值
* done: 是否已经迭代完成，完成返回true，未完成返回false
### Iterator定义和使用例子
```js
let obj = {
  start: [1,3,2],
  end: [1,9,8],
  [Symbol.iterator]() {
    let self = this;
    let index = 0;
    let arr = self.start.concat(self.end);
    let len = arr.length;
    return {
      next() {
        if (index<len) {
          return {
            value: arr[index++],
            done: false
          }
        } else {
          return {
            value: arr[index++],
            done: true
          }
        }
      } 
    }
  }
}

for (let key of obj) {
  console.log(key);
}
```
### 特殊的定义技巧

Generator函数返回的就是iterator对象，所以`[Symbol.iterator]`属性可以直接接收一个Generator函数