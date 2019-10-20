一共有8个共4对生命周期函数

#### 第一对：创建

* beforeCreate：组件创建前调用
* created：组件创建完毕时调用

#### 第二对：挂载

* beforeMount：组件挂载前调用
* mounted：组件挂载完毕时调用

#### 第三堆：更新

* beforeUpdate：组件更新前调用
* updated：组件更新完毕时调用

#### 第四对：销毁

* beforeDestroy：执行vm.$destroy()时调用
* destroyed：组件销毁完毕时调用

![生命周期](./image/lifecycle.png)