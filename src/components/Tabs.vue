<template>
  <div class="tabs">
    <div class="tab-link">
	  <div v-bind:style="tabBarStyle" class="tab-bar-container">
        <div class="tab-bar"></div>
	  </div>
	  <div class="tab-nav">
	    <div v-bind:class="{ active: item.tabKey == activeKey }" v-on:click="switchTab(item.tabKey)" class="tab-tab" v-for="item in items">{{item.tab}}</div>
	  </div>
	  <slot></slot>
	</div>
  </div>
</template>

<script>
export default {
  name: 'tabs',
  // 声明 props
  props: ['defaultActiveKey'],
  data () {
    return {
      items: [],
      tabBarStyle: {},
      activeKey: this.defaultActiveKey
    }
  },
  mounted () {
    console.log(this.$children)
    var itemSize = parseInt(this.$children.length)
    this.tabBarStyle.top = 0
    this.tabBarStyle.left = 0
    this.tabBarStyle.right = 100 - 100 / itemSize + '%'
    this.tabBarStyle.transform = 'translate3d(0,0,0)'
    this.items = this.$children
  },
  methods: {
    switchTab (key) {
      key = parseInt(key)
      console.log(key)
      this.activeKey = key
      this.tabBarStyle.transform = 'translate3d(' + (key - 1) * 100 + '%,0,0)'
      for (var i = 0; i < this.$children.length; i++) {
        this.$children[i].switchTabHandle(key)
      }
    }
  }
}
</script>

<style scoped>
  .tab-link{
    position: relative
  }
  .tab-bar-container{
    transition: transform 1s;
    position: absolute;
	padding: 0 20px;
  }
  .tab-bar{
    background: #f37327;
	height: 4px;
  }
  .tab-nav{
    display: flex;
  }
  .tab-tab{
    height: 40px;
	line-height: 40px;
	text-align: center;
	flex: 1;
  }
  .active{
    color: #f37327;
  }
</style>
