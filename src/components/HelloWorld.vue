<template>
  <div class="hello">
    <h1 @click="send">组件通信{{ $store.state.time }}</h1>
    <h1 @click="handleclick">{{ msg }}</h1>
    <p>
      For a guide and recipes on how to configure / customize this project,
      <br>check out the
      <a
        href="https://cli.vuejs.org"
        target="_blank"
        rel="noopener"
      >vue-cli documentation</a>.
    </p>

    <h3>Ecosystem</h3>
    <ul>
      <li>
        <a href="https://router.vuejs.org" target="_blank" rel="noopener">vue-router</a>
      </li>
      <li>
        <a href="https://vuex.vuejs.org" target="_blank" rel="noopener">vuex</a>
      </li>
      <li>
        <a
          href="https://github.com/vuejs/vue-devtools#vue-devtools"
          target="_blank"
          rel="noopener"
        >vue-devtools</a>
      </li>
      <li>
        <a href="https://vue-loader.vuejs.org" target="_blank" rel="noopener">vue-loader</a>
      </li>
      <li>
        <a href="https://github.com/vuejs/awesome-vue" target="_blank" rel="noopener">awesome-vue</a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: {
      type: String,
      default: '哈哈，子组件'
    }
  },
  data() {
    return {}
  },
  methods: {
    handleclick() {
      console.log(this.$props.msg)
      const data = { age: 23, sex: 'girl' }
      this.$emit('getVal', data) // 子组件触发父组件的getVal()事件，并传递参数data给父组件
    },
    conMsg() {
      console.log('子组件的方法')
    },
    send() {
      const str = '接受到了兄弟组件传的信息了'
      // this.$root.$emit("getMsg", str); //$root为根组件，可以用它实现兄弟组件之间的通信

      this.$eventBus.$emit('getMsg', str)
      this.$store.commit({
        type: 'addNum',
        number: 2
      }) // 提交 mutation
      this.$store.commit('getTime')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
h3 {
  margin: 40px 0 0;
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
