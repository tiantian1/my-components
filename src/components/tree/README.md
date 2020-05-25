    无限层级部门树，使用递归实现。

1. 使用eventBus解决 爷爷组件和孙子组件之间的传值。
- main.js 里注册eventBus
```js
    Vue.prototype.$EventBus=new Vue();
```
- 组件中向外传值使用
```js
    this.$EventBus.$emit("chooseItem", item); 
```
- 在父组件中mounted中监听事件接受值
```js
    this.$EventBus.$on('chooseItem',res=>{
          console.info("selected:",res);
    })
```
2. 解决`chooseItem`多次触发的问题
```js
 beforeDestroy() {
    this.$EventBus.$off("chooseItem");
  }
```