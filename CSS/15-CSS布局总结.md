> 参考自 https://www.cnblogs.com/yanayana/p/7066948.html

### 布局方案

| 方案名称   | 定义                                                         | 实现                                                         |
| ---------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 静态布局   | 静态布局指的是不管浏览器尺寸具体是多少，网页始终按照原始页面大小进行显示 | ①使用绝对长度单位px定义宽高<br>②设置页面居中                 |
| 流式布局   | 流式布局指的是页面元素的宽度使用百分比按照屏幕分辨率进行适配调整，屏幕分辨率变化时，页面里元素的大小会变化而但布局不变 | ①使用百分比定义宽度，使用rem或em等相对长度单位定义高度<br>②配合min-width，max-width控制尺寸流动范围以免布局过大或者过小<br>③通过meta标签，设置视口为理想视口 |
| 自适应布局 | 自适应布局指的是分别为不同屏幕分辨率的终端设备提供不同的页面 | 使用媒体查询来为不同屏幕分辨率的终端设备切换特定的页面       |
| 响应式布局 | 响应式布局指的是确保一个页面在所有终端上都能显示出令人满意的效果 | 使用媒体查询来为不同屏幕分辨率的终端设备提供特定的CSS样式    |

-------------------------------------

### 布局技术

#### 长度单位
* 绝对单位px
* 相对单位em、rem
* 宽度百分比

#### 盒子布局

| 盒子布局技术  | 优点                     | 缺点                                 |
| ------------- | ------------------------ | ------------------------------------ |
| table表格系统 | 兼容性好                 | API少，很难用                        |
| 浮动+定位     | 兼容性好                 | 使用麻烦，需要较多计算，需要清除浮动 |
| flex弹性盒子  | 使用方便，很适合一维布局 | 兼容性一般                           |
| grid网格系统  | 使用方便，很适合二维布局 | 兼容性不好                           |