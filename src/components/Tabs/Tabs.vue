<template>
  <div class="tabs" :id="id">
    <slot></slot>
  </div>
</template>

<script>
  import Eventable from '../../mixins/eventable'

  export default {
    name: 'tabs',

    mounted () {
      this.init()
    },

    activated () {
      this.init()
    },

    methods: {
      init () {
        if (window.location.hash === '') {
          return
        }

        const active = window.location.hash.substr(1)
        
        this.$children.forEach(i => {
          if (active === i.$el.id) {
            this.$rubik.bridge.pub('tab:open', i.$el.id)
          }
        })
      }
    }
  }
</script>