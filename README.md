# vue2-modal-bootstrap

> vue2 modal bootstrap. support render custom component!

```javascript
import Vue from 'vue'
import VueModalPlugin from 'vue2-modal-bootstrap'
Vue.use(VueModalPlugin)

var vm = this.$modal({
    title: '确定',
    message: '操作后无法撤销',
    prompt: true,
    autoClose: false,
    okText: '好',
    cancelText: '取消',
    size: 'sm',
    callback: function (value) {
      console.log(value)
    },
    data: {
      text: 'this is custom component'
    },
    events: {
      click () {
        console.log('click')
      }
    }
  },
  {
    props: {
      text: ''
    },
    template: '<div @click="$emit(\'click\')">{{text}}</div>'
  }
)
```

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```

For detailed explanation on how things work, consult the [docs for vue-loader](http://vuejs.github.io/vue-loader).
