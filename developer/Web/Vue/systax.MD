1. 模板语法
除了基本的 {{message}} 渲染值外, Vue还支持更多的js表达式. 
```
// html 例如: 
<span>{{number+1}} </span>
{{ ok ? 'YES' : 'NO' }}
// 属性
<div v-bind:id="'list-' + id"></div>


//注意,每个绑定都只能包含单个表达式，所以下面的例子都不会生效
<!-- 这是语句，不是表达式 -->
{{ var a = 1 }}

<!-- 流控制也不会生效，请使用三元表达式 -->
{{ if (ok) { return message } }}
```
2. Vue内置属性缩写, v-
```
// v-bind缩写
<!-- 完整语法 -->
<a v-bind:href="url">...</a>

<!-- 缩写 -->
<a :href="url">...</a>

<!-- 动态参数的缩写 (2.6.0+) -->
<a :[key]="url"> ... </a>

//v-on缩写
<!-- 完整语法 -->
<a v-on:click="doSomething">...</a>

<!-- 缩写 -->
<a @click="doSomething">...</a>

<!-- 动态参数的缩写 (2.6.0+) -->
<a @[event]="doSomething"> ... </a>
```

3. 计算属性 computed
和data中渲染赋值类似, 而计算属性是调用方法获取值
```
<div id="example">
  <p>Original message: "{{ message }}"</p>
  <p>Computed reversed message: "{{ reversedMessage }}"</p>
</div>

var vm = new Vue({
  el: '#example',
  data: {
    message: 'Hello'
  },
  computed: {
    // 计算属性的 getter
    reversedMessage: function () {
      // `this` 指向 vm 实例
      return this.message.split('').reverse().join('')
    }
  }
})

// 定义为方法

methods: {
  reversedMessage: function () {
    return this.message.split('').reverse().join('')
  }
}

<p>Reversed message: "{{ reversedMessage() }}"</p>


```
4. 侦听器

```
var watchExampleVM = new Vue({
  el: '#watch-example',
  data: {
    question: '',
    answer: 'I cannot give you an answer until you ask a question!'
  },
  watch: {
    // 如果 `question` 发生改变，这个函数就会运行
    question: function (newQuestion, oldQuestion) {
      this.answer = 'Waiting for you to stop typing...'
      // TODO 这里定义延迟,可以等待异步请求.

    }
    }
}
  
```

5. css样式
v-bind:class 语法格式: 
```

1. {样式1,样式2}
2. {class样式[: boolean是否激活],... }
 <div class="static" v-bind:class="{ active: isActive,'text-danger': hasError }"></div>
3. [样式1,样式2]
4. [{样式1:是否激活},样式2]
5. [isActive: 样式1:样式2]  // 表达式


```
6. 内联样式
v-bind:style
```

<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
// 多项值
<div :style="{ display: ['-webkit-box', '-ms-flexbox', 'flex'] }"></div>

```

7. 条件渲染
v-if
```
<div v-if="条件表达式"></div>
<div v-else-if="条件表达式"></div>
<div v-else="条件表达式"></div>

v-else，v-else-if 也必须紧跟在带v-if的元素之后.


// 示例:
<div v-else="loginType === 'weChat'"></div>

```
8. v-show
通过css样式进行控制显示,不同于v-if, v-show始终渲染,然后切换样式进行显示隐藏.
```
<div v-show='ok'>
```

9. v-for
语法: v-for=[value of values]
```
<ul id="v-for-object" class="demo">
  <li v-for="value in object">
    {{ value }}
  </li>
</ul>
// 也支持
<div>
  <span v-for="n in 10">{{ n }} </span>
</div>
```
10. v-bind 
修改html的属性