<template>
  <div v-bind:class="{ activeContent: tabKey == activeKey, notActive: tabKey != activeKey}">
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: 'tabPane',
  // 声明 props
  props: ['tab', 'tabKey'],
  data () {
    return {
      activeKey: ''
    }
  },
  beforeMount () {
    this.activeKey = this.$parent.activeKey || this.$parent.defaultActiveKey
  },
  mounted () {
    console.log('==2', this.$parent.activeKey)
  },
  methods: {
    switchTabHandle (key) {
      this.activeKey = key
    }
  }
}
</script>

<style scoped>
  .activeContent{
    display: block
  }
  .notActive{
    display: none
  }
</style>
