<template>
<div class="component-modal modal fade in">
  <div class="modal-backdrop fade in"></div>
  <div class="modal-dialog" :class="'modal-'+size">
    <button class="close" @click="close">
      <span aria-hidden="true">×</span>
    </button>
    <div class="modal-content">
      <header class="modal-header" v-if="title" ref="header">{{title}}</header>
      <div class="modal-body">
        <div class="message-content" v-if="message||prompt">
          <p v-if="message">{{message}}</p>
          <input type="text" class="form-control" v-model="inputValue" >
        </div>
      </div>
      <modal-body v-if="$options.components.ModalBody" v-bind="data" v-on="events" ref="body" class="modal-body"></modal-body>
      <footer class="modal-footer" ref="footer">
        <button class="btn btn-primary" @click="postive">{{okText}}</button>
        <button class="btn btn-default" @click="negative">{{cancelText}}</button>
      </footer>
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: 'Modal',
  props: {
    data: {
      type: Object,
      default () {
        return {}
      }
    },
    events: {
      type: Object,
      default () {
        return {}
      }
    },
    size: {
      type: String,
      default: 'md'
    },
    title: {
      type: String,
      default: ''
    },
    okText: {
      type: String,
      default: 'ok'
    },
    cancelText: {
      type: String,
      default: 'cancel'
    },
    message: {
      type: String,
      default: ''
    },
    prompt: {
      type: Boolean,
      default: true
    },
    autoClose: {
      type: Boolean,
      default: true
    },
    callback: {
      type: Function,
      default () {
        return function () {}
      }
    }
  },
  data () {
    return {
      inputValue: ''
    }
  },
  methods: {
    close () {
      this.$emit('close')
      this.callback(this.inputValue, 'close')
      this.$destroy()
    },
    postive () {
      this.$emit('postive', this.inputValue)
      this.callback(this.inputValue, 'positive')
      this.autoClose && this.$destroy()
    },
    negative () {
      this.$emit('negative', this.inputValue)
      this.callback(this.inputValue, 'negative')
      this.autoClose && this.$destroy()
    }
  },
  mounted () {
    document.body.classList.add('modal-open')
  },
  beforeDestroy () {
    this.$el.parentNode.removeChild(this.$el)
  },
  destroyed () {
    document.body.classList.remove('modal-open')
  }
}
</script>

<style>
.component-modal.modal {
  display: block;
}
.modal .modal-backdrop {
  z-index: 0;
}
.modal .close {
  position: relative;
  z-index: 1;
  margin-right: 8px;
  margin-top: 6px;
}
.modal .modal-full {
  width: 100%;
  height: 100%;
  margin: 0;
  border-radius: 0;
}
.modal .modal-full .modal-content {
  width: 100%;
  height: 100%;
  border: none;
  border-radius: 0;
}
</style>
