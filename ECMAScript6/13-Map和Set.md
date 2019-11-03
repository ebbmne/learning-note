### Map
#### 定义

Map是哈希表

#### 区别

Map与传统对象的区别：Map的键可以是任意类型

#### 声明和初始化

##### 空的Map

```js
const map = new Map();
```

#### 由数组进行初始化

```js
const arr = [[true, 1],[2, 2],["c", 3]];
const map = new Map(arr);
```

#### 增删改查清空

```js
map.set("key","value"); // 增，改
map.delete("key"); // 删
map.has("key"); // 查
map.clear();
```

#### 遍历

```js
for (let [key, value] of map) {
  console.log("key:", key, "value:", item);
}
// 等价于
for (let [key, value] of map.entries()) {
  console.log("key:", key, "value:", item);
}

for (let value of map.values()) {
  console.log("value:", value)
}

for (let key of list.keys()) {
  console.log("key:", key)
}
```

------------------------------------------

### WeakMap

API与Map完全相同：set, delete, has, clear

WeakMap和Map区别：WeakMap只能是引用，不能是基础类型

WeakSet不参与垃圾回收装置，即WeakSet存的引用指向的对象可能会被垃圾回收机制回收

-------------------------------------------------------

### Set

#### 定义

Set是集合，里面不可以放重复元素，很好的去重工具

#### 声明和初始化

##### 声明空集合

```js
const set = new Set();
```

#### 用数组进行初始化

```js
let arr = [1,2,3,4,5];
let set = new Set(arr);
```

增删查清空
```js
set.add(1); // 增，只接收一个参数
set.delete(1); // 删，只接收一个参数
set.has(1); // 查，只接收一个参数
set.clear(); // 清空
```

遍历
```js
for (let value of set.values()) {
  console.log("value:", value)
}
// 等价于
for (let key of set.keys()) {
  console.log("value:", key)
}
// 等价于
for (let item of set) {
  console.log("value:", item)
}
// 等价于
set.forEach((item) => { console.log("value", item) })
```

----------------------------------------------------------

### WeakSet

API与Set完全相同：add, delete,has,clear

与Set区别：WeakSet只能存引用，不能存基础类型 

WeakSet不参与垃圾回收装置，即WeakSet存的引用指向的对象可能会被垃圾回收机制回收

