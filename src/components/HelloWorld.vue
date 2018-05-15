<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h1>Computed reversed message: {{ reversedMsg }}</h1>
    <!-- lazy修饰符：懒加载，失去焦点后才触发双向绑定数据同步；trim修饰符：去掉首位空字符串 -->
    <input v-model.lazy.trim="msg">
    <ol>
      <li>测试v-for：</li>
      <!-- key的作用主要是为了高效的更新虚拟DOM（ng中的track-by）
      详解：https://www.zhihu.com/question/61064119/answer/187145550
       -->
      <li v-for="(todo,index) in todos" :key="todo.id">
        {{index}}-{{ todo.text }}
      </li>
    </ol>
    <!-- template标签可以作为一个虚拟标签，在上面统一写指令 -->
    <template v-if="isBtnShow">
      <!-- 调用方法可以没括号，没括号同样可以在方法中获得event；有括号的叫内敛处理器 -->
      <button v-on:click="reverseMessage">逆转消息</button>
      <a v-bind:href="'http://www.baidu.com'">testBind</a><!-- :href -->
      <a v-on:click="testClick">testClick</a><!-- @click -->
    </template>
    <!-- v-if和v-show的注意事项
    Vue为了高效地渲染元素，会尽可能复用已有元素，所以v-if切换的时候，可能还是一个元素，
    必要的时候加属性key="xxx"来禁止重用，当然，加上v-model能达到同样的效果；
    v-show不可使用template标签，不可后接v-else -->

   
    <!-- 三种 v-bind:class的写法
    <div v-bind:class="classObject"></div>
    <div v-bind:class="{ active: isActive, 'text-danger': hasError }">
    <div v-bind:class="[isActive ? activeClass : '']"></div> -->
    <!-- 三种 v-bind:style的写法
    <div v-bind:style="styleObject"></div>
    <div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
    <div v-bind:style="[baseStyles, overridingStyles]"></div> -->

    <select v-model="selected">
      <option v-for="option in options" v-bind:value="option.value">
        {{ option.text }}
      </option>
    </select>
    <span>Selected: {{ selected }}</span>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  
  data() {
    return {
      msg: "Hello world, Vue.js",
      // 列表展示
      todos: [
        { id:1, text: '学习 JavaScript' },
        { id:2, text: '学习 Vue' },
        { id:3, text: '整个牛项目' }
      ],
      // 测试v-if
      isBtnShow: true,
      // 下拉框回显
      selected: 'B',
      options: [
        { text: 'One', value: 'A' },
        { text: 'Two', value: 'B' },
        { text: 'Three', value: 'C' }
      ]
    };
  },
  methods: {
    reverseMessage: function () {
      this.msg = this.msg.split('').reverse().join('')
    },
    testClick: function () {
      console.log(event)
      alert("test");
    }
  },
  // 计算属性
  // 和方法的区别：计算属性是基于它们的依赖进行缓存的，如果被依赖的值没变化，就不会调用计算，而是直接返回之前计算的缓存
  // computed的妙用：特定场景替代watch监听器，比如监听A和B，计算C=A+B，这里直接C:function(){retrurn A+B}
  computed: {
    reversedMsg: function () {
      // `this` 指向 vm 实例
      return this.msg.split('').reverse().join('')
    },
    // 完整的getter和setter
    // reversedMsg2: {
    //   get: function () {
    //     return this.firstName + ' ' + this.lastName
    //   },
    //   set: function (newValue) {
    //     var names = newValue.split(' ')
    //     this.firstName = names[0]
    //     this.lastName = names[names.length - 1]
    //   }
    // }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
