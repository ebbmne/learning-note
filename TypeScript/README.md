> TypeScript是ECMAScript的超集，即兼容JavaScript，故只记录TypeScript对ECMAScript增强的地方



## 类型

### 类型注解

可以指定变量、常量、参数和返回值等的类型，用于编译时进行类型检查，当值不符合注解的类型时，TypeScript会报错

```typescript
// 注解变量、常量类型
let a: string = "typescript"; //ok
let b: string = 123; // error
const c: boolean = true; // ok

// 注解参数类型和返回值类型
function func(d: string): void {}
```

数组的类型注解方式

```typescript
// 普通方式 + 数组元素均为同一类型
let arr1: number[] = [1,2,3];

// 泛型方式 + 数组元素均为同一类型
let arr2: Array<number> = [1,2,3];

// 泛型方式 + 数组元素均为同一类型 + 只读数组
// 一旦定义就不能修改数组元素的值
// 只读数组不可以赋值给普通数组类型，除非使用类型断言
let arr3: ReadonlyArray<number> = [1,2,3];

// 数组元素不为同一类型，称为元组，要求类型和数量都配匹配
let arr4: [number, string, boolean] = [123, "456", true];
```

<br/>

### 类型系统增强

- number, string, boolean, symbol 与 ECMAScript 一样

- null, undefined

  默认情况下，null和undefined是所有类型的子类型，即null和undefined可以赋值给任意类型 
  
- object

  表示非原始类型，也就是可以接受除 boolean, number, string, symbol 之外的类型

- any

  新增类型，表示任意类型

  作用：在不知道具体类型时使用，比如来自第三方代码库的类型或者DOM元素

- void

  新增类型：表示没有任何类型

  作用：一般只用于函数返回值

  注意：可以接受 null和undefined，因为 null 和 undefined 是任意类型的子类型

- never

  新增类型：表示那些不可能拥有的类型

  作用：用于定义抛出异常的函数的返回值

  注意：
  - 没有类型是never的子类型，即任何类型也不可以赋值给never类型（除了never类型本身）
  - never是任何类型的子类型，即never可以赋值任何类型，类似undefined和null

- enum

  新增类型：枚举

  作用：为数值或字符串提供见名知意的名字

  定义语法

  ```typescript
  enum 枚举名 {
      枚举值,
      枚举值 = 具体值,
      枚举值
  }
  ```

  例子

  ```typescript
  // 如果不设置枚举值对应具体值，则默认从0开始的序号
  enum Color {
      Red,
      Green,
      Blue
  }
  
  enum Gender {
      Man = 1,
      Woman = 8
  }
  
  console.log(Gender.Man);
  ```

  反取：可以由索引获取枚举值

  ```typescript
  enum Gender {
      Man = "male",
      Woman = "female"
  }
  
  let genderName: string = Gender[1];
  console.log(genderName); // Woman
  ```
  <br/>

### 类型断言

在一些情况下，你会比TypeScript更加了解某个值的具体类型，这时可以使用类型断言，让TypeScript不进行类型检查

类型断言类似于强制类型转换，但不会进行类型的检查

类型断言用法：

* 方式一：使用尖括号语法

  ```typescript
  let obj: any = "typescript";
  let str: string = (<string>obj);
  ```

* 方式二：使用as关键字（推荐）

  ```typescript
  let obj: any = "typescript";
  let str: string = (obj as string);
  ```

<br/>
    

## 接口

接口是一种规范，用于制定标准，从而约束对象的结构和组成

### 约束属性

定义语法

```typescript
interface 接口名 {
    属性名: 属性类型;
    属性名: 属性类型;
    ...
    属性名: 属性类型;
} 
```

例子

```typescript
interface Circle {
	color: string;
    radius: number;
}
```

注意：接口约束是严格的，即当对象是接口类型时，它拥有的属性和属性值的类型必须和接口定义完全一样，不能多不能少



#### 可选属性

默认情况下，被接口约束的对象拥有的属性和属性值类型必须和接口定义完全一样，不能多不能少，但使用可选属性后，对象可以没有可选属性

在需要设置为可选属性的接口定义处上加上 `?` 即可将属性设置为可选属性

```typescript
interface Circle {
    color: string;
    radius?: number;
}

let a: Circle = {color: "red", radis: 100}; // ok
let b: Circle = {color: "blue"}; // ok
```



#### 只读属性

用于设置在被接口约束的对象在第一次赋值后，就不能再进行值修改

使用关键字 readonly 进行修饰

```typescript
interface FullName {
    readonly firstName: string;
    readonly secondName: string;
}

let p: FullName = {firstName: "张", secondName: "三"};
p.firstName = "李"; // 报错
```



#### 绕过接口检查的方法

方法一：使用类型断言，不让TypeScript进行检查

```typescript
createCircle({color:"red", abc: 100} as CircleConfig);
```

方法二：传入对象的引用，而不是具体的对象

```typescript
let circle = {color:"red", abc: 100, a: 'q', c:10};
let myCircle = createCircle(circle);
```

方法三：通过字符串的索引签名

```typescript
interface Circle {
    color?: string;
	radius?: number;
    [propsName: string]: any;
}

createCircle({color:"red", abc: 100, a: 'q', c:10});
```

<br/>

### 约束可索引类型

在接口定义索引的类型和索引值的类型

```typescript
interface StrArr {
    [index: number]: string
}

let myArr: StrArr = ["type", "script"];
```

<br/>

### 约束函数

在接口定义函数签名

```typescript
interface 接口名 {
	(参数列表): 返回值;
} 
```

例子

```typescript
interface CompareFunc {
    (first: number, last: number): boolean //函数签名
}

// 写法一：
let myCompare1: CompareFunc = function (first: number, last: number): boolean {
    return first > last;
}

// 写法二：
let myCompare2: CompareFunc = function (a, b) {
    return a > b;
}
myCompare1(1,2) // ok
myCompare2("123",true) // error
```

<br/>

### 约束类

接口约束类就是指类实现接口

```typescript
interface 接口名 {}

class 函数名 implements 接口名 {}
```

<br/>

### 接口继承

接口也可以相互继承，接口继承相当于将父接口的内容复制到子接口中

```typescript
interface Shape {
  color: string
}

interface Square extends Shape {
  sideLength: number
}

let square = {} as Square;
square.color = 'blue';
square.sideLength = 10;
```

接口可以多继承

```typescript
interface Cat extends Animal, Mammal {}
```



## 面向对象

## 函数

## 泛型

## 高级特性

