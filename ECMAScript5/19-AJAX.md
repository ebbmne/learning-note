### Ajax概念 

Ajax是一种在不刷新（不提交表单）的前提下，可以和服务器进行数据交互的技术

### Ajax读取到的数据类型

Ajax 读取到的数据全部都是字符串类型，可以使用`JSON.parse`解析成字符串

### 阻止浏览器缓存

浏览器是根据 url 进行缓存的，所以可以通过在 url 后加上时间戳的方法来实现阻止缓存

### Ajax原理

> 创建XMLHtpRequest对象 -> 连接到服务器 -> 发送请求 -> 接收返回值

```js
// 1. 创建 XMLHttpRequest 对象
const oAjax = new XMLHttpRequest(); // 不兼容 IE 6

// 2. 连接到服务器
// open(请求方法，请求地址，是否异步传输)
oAjax.open("GET", "https://www.test.com/aaa.txt",  true);

// 3. 发送请求
oAjax.send();

// 4. 接收返回值
oAjax.onreadystatechange = function() {
// 0 : 刚刚创建完 XMLHttpRequest
// 1 : 已调用 send 方法，正在发送请求和接收响应内容
// 2 : send()完成，已接收到服务器返回的全部响应内容
// 3 : 正在解析响应内容
// 4 : 传输完成（成功或失败），可以在客户端调用
  if (oAjax.readyState === 4) {
    if (oAjax.status === 200) { // 状态码
      console.log(oAjax.responseText); // 返回的字符串
    } else {
      console.log("failed");
    }
  }
}
```

