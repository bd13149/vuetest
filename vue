1.声明式渲染
数据：{{  }}
var app = new Vue({
    el: '#app',
    data: {
      message: 'Hello Vue!'

    }
  });
  el：元素id
  data中的message 用来渲染
2.v-
v-bind 属性被称为指令
指令带有前缀 v-，以表示它们是vue.js提供的特殊属性
这个指令的简单含义是：将这个元素节点的title属性和vue实例的message属性绑定到一起。
<span v-bind:title="message">
    Hover your mouse over me for a few seconds to see my dynamically bound title!
</span>
var app2 = new Vue({
    el: '#app-2',
    data: {
      message: 'You loaded this page on ' + new Date()
    }
  })
  app2.message = 'some new message'
3.不仅可以绑定 DOM 文本到数据，也可以绑定 DOM 结构到数据
app3.seen = false 元素就会消失
v-if="seen"
4.v-for：可以绑定数据到数组来渲染一个列表
5.v-on:click="test"
6.v-model 使得在表单输入和应用状态中做双向数据绑定变得非常轻巧
7.v-text：类型 string 更新元素的textContent。如果要更新部分的textContent，需要使用{{ Mustache }}插值
8.v-show：根据表达式之真假值，切换元素的 display css属性.注意 v-show 不支持 <template> 语法。
9.v-else：前一兄弟元素必须有v-if 或 v-else-if

10.v-for: Array|Object|number|string
  10.1基于源数据多次渲染元素或模板块，必须用特定的语法 alias in expression ，为当前遍历的元素提供别名：
  <div v-for="item in items">
    {{ item.text }}
  </div>
  10.2另外也可以为数组索引指定别名(或者用于对象的键)：
  <div v-for="(item, index) in items"></div>
  <div v-for="(val, key) in object"></div>
  <div v-for="(val, key, index) in object"></div>
  10.3v-for默认行为试着不改变整体，而是替换元素。迫使其中心排序的元素，您需要提供一个key的特殊属性：
  <div v-for="item in items" :key="item.id">
    {{ item.text }}
  </div>
  10.2在 v-for 块中，我们拥有对父作用域属性的完全访问权限。 v-for 还支持一个可选的第二个参数为当前项的索引。

11 if与show
11.1v-if 是真实的条件渲染，因为它会确保条件块在切换当中适当地销毁与重建条件块内的事件监听器和子组件。
11.2v-if 也是惰性的：如果在初始渲染时条件为假，则什么也不做——在条件第一次变为真时才开始局部编译（编译会被缓存起来）。
11.3相比之下， v-show 简单得多——元素始终被编译并保留，只是简单地基于 CSS 切换。
11.4一般来说， v-if 有更高的切换消耗而 v-show 有更高的初始渲染消耗。因此，如果需要频繁切换使用 v-show 较好，如果在运行时条件不大可能改变则使用 v-if 较好。

12 if和for：当与v-for一起使用时，v-for具有比v-if更高的优先级

13 v-if 如果我们想切换多个元素呢？此时我们可以把一个 <template> 元素当做包装元素，并在上面使用 v-if

14.数组更新监测
push()/pop()/shift()/unshift()/splice()/sort()/reverse()

15.重塑数组
filter()/concat()/slice() 这些不会改变原始数组，但总是返回一个新数组，当使用非变异方法时，可以用新数组替换旧数组
example1.items = example1.items.filter(function (item){
  return item.message.match(/Foo/)
})

16.当利用索引直接设置一个项目时，
// Vue.set
Vue.set(example1.items, indexOfItem, newValue)
// Array.prototype.splice`
example1.items.splice(indexOfItem, 1, newValue)

17.修改数组的长度
example1.items.splice(newLength)

18.使用JavaScript表达式
{{ number + 1 }}
{{ ok? 'yes':'no }}
{{ message.split('').reverse().join('') }}
<div v-bind:id = " 'list-' + id "></div>
每个绑定都只能包含单个表达式
<!-- 这是语句，不是表达式 -->
{{ var a = 1 }}
<!-- 流控制也不会生效，请使用三元表达式 -->
{{ if (ok) { return message } }}

19.修饰符，用“ . ”指明特殊的后缀，用于指出一个指令应该以特殊的方式绑定。例如，.prevent修饰符告诉v-on指令对于
触发的事件调用event.preventDefault()：
<form v-on:submit.prevent="onSubmit"></form>

20.除了 data 属性， Vue 实例暴露了一些有用的实例属性与方法。这些属性与方法都有前缀 $，以便与代理的 data 属性区分。

var data = { a: 1 }
    var vm = new Vue({
        el: '#example',
        data: data
    })
    vm.$data === data // -> true
    vm.$el === document.getElementById('example') // -> true
    // $watch 是一个实例方法
    vm.$watch('a', function (newVal, oldVal) {
        // 这个回调将在 `vm.a`  改变后调用
    })

注意，不要在实例属性或者回调函数中（如 vm.$watch('a', newVal => this.myMethod())）使用箭头函数。
因为箭头函数绑定父上下文，所以 this 不会像预想的一样是 Vue 实例，而是 this.myMethod 未被定义。

21.如果在实例创建之后添加新的属性到实例上，它不会处罚视图更新。
   vue实例暴露了一些有用的实例属性与方法，这些属性与方法都有前缀$ ,以便与代理的data属性区分。
   var data = { a: 1 }
   var vm = new Vue({
     el: '#example',
     data: data
   })

   vm.$data === data //true
   vm.$el === document.getElementById('example') // -> true
   // $watch 是一个实例方法
   vm.$watch('a',function(newVal,oldVal){
      // 这个回调将在 `vm.a`  改变后调用
   })

22.“Mustache” 语法（双大括号）的文本插值

23.过滤器：应该被添加在mustache插值的尾部，{{ message | capitalize }},
   过滤器函数总接受表达式的值作为第一个参数
   new Vue({
     // ...
     filters: {
       capitalize: function (value) {
         if (!value) return ''
         value = value.toString()
         return value.charAt(0).toUpperCase() + value.slice(1)
       }
     }
   })
   过滤器可以串联：{{ message | filterA | filterB }}
   过滤器是 JavaScript 函数，因此可以接受参数：{{ message | filterA('arg1', arg2) }}

24.v-bind 指令被用来响应地更新 HTML 属性：
   <a v-bind:href="url"></a>
   在这里href是参数，告知v-bind指令将该元素的href属性与表达式url的值绑定

25.v-on 指令，它用于监听 DOM 事件
   <a v-on:click="doSomething">
   在这里参数是监听的事件名。我们也会更详细地讨论事件处理。

26.缩写：
    v-bind缩写
   <!-- 完整语法 -->
   <a v-bind:href="url"></a>
   <!-- 缩写 -->
   <a :href="url"></a>

    v-on缩写
   <!-- 完整语法 -->
   <a v-on:click="doSomething"></a>
   <!-- 缩写 -->
   <a @click="doSomething"></a>































