1. 组件
组件的data必须是一个函数,因此每个实例可以维护一份被返回对象的独立的拷贝
```
Vue.component('button-counter', {
  data: function () {
    return {
      count: 0
    }
  },
  template: '<button v-on:click="count++">You clicked me {{ count }} times.</button>'
})
```


参考:
* [Vue组件](https://cn.vuejs.org/v2/guide/components.html)