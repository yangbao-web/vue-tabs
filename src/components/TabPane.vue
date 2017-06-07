<template>
  <div class="tabpane" v-bind:style="sliderItemStyle" v-bind:class="{ activeContent: tabKey == activeKey, notActive: tabKey != activeKey}">
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
      activeKey: '',
      pageWidth: '',
      sliderItemStyle: {}
    }
  },
  beforeMount () {
    this.activeKey = this.$parent.activeKey || this.$parent.defaultActiveKey
  },
  mounted () {
    var tabContainerWidth = parseInt(this.$parent.$refs.tabContainer.offsetWidth)
    this.sliderItemStyle.width = tabContainerWidth + 'px'
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
    //display: none
  }
  .tabpane{
    float: left;
    width: 100%;
  }
</style>
