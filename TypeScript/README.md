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

数组的定义方式

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

### 类型系统增强

- number, string, boolean, symbol 与 ECMAScript 一样

- null, undefined

  - 默认情况下，null和undefined是所有类型的子类型
  - 即null和undefined可以赋值给任意类型 

- object

  - 表示非原始类型，也就是可以接受除 boolean, number, string, symbol 之外的类型

- any

  - 新增类型，表示任意类型
  - 作用：在不知道具体类型时使用，比如来自第三方代码库的类型或者DOM元素

- void

  - 新增类型：表示没有任何类型
  - 作用：一般只用于函数返回值
  - 注意：可以接受 null和undefined，因为 null 和 undefined 是任意类型的子类型

- never

  - 新增类型：表示那些不可能拥有的类型
  - 作用：用于定义抛出异常的函数的返回值
  - 注意：
    - 没有类型是never的子类型，即任何类型也不可以赋值给never类型（除了never类型本身）
    - never是任何类型的子类型，即never可以赋值任何类型，类似undefined和null

- enum

  - 新增类型：枚举

  - 作用：为数值或字符串提供见名知意的名字

  - 定义：

    ```typescript
    enum 枚举名 {
        枚举值,
        枚举值,
        枚举值
    }
    
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
    ```

  - 反取：可以由索引获取枚举值

    ```typescript
    enum Gender {
        Man = "male",
        Woman = "female"
    }
    
    let genderName: string = Gender[1];
    console.log(genderName); // Woman
    ```

    



## 接口

## 面向对象

## 函数

## 泛型

## 高级特性

