### 检测网络连接状态

window上的两个事件online和offline

online: 用户网络连接时被调用

offline: 用户网络断开时被调用
```html
<script>
  window.addEventListener("online", function() {
    alert("网络已连接");
  })  
    
  window.addEventListener("offline", function() {
    alert("网络连接失败")  
  })
</script>
```