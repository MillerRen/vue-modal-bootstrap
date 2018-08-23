<template>
  <div id="app">
  </div>
</template>

<script>

export default {
  name: 'app',
  mounted () {
    var vm = this.$modal({
        title: '确定',
        message: '操作后无法撤销',
        prompt: true,
        autoClose: false,
        okText: '好',
        cancelText: '取消',
        callback: function (value) {
          console.log(value)
        },
        data: {
          text: 'this is custom component'
        }
      },
      {
        props: {
          text: ''
        },
        template: '<div>{{text}}</div>'
      }
    )
    vm.$on('postive', (value) => {
      console.log(value)
      value&&vm.$destroy()
    })
    vm.$on('negative', (value) => {
      console.log(value)
      vm.$destroy()
    })
    vm.$on('close', () => {
      console.log('close')
    })
  }
}
</script>

<style>
@import "~bootstrap/dist/css/bootstrap.css";
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
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
