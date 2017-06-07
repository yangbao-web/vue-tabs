<template>
  <div class="tabs">
    <div class="tab-link">
	  <div v-bind:style="tabBarStyle" class="tab-bar-container">
        <div class="tab-bar"></div>
	  </div>
	  <div class="tab-nav">
	    <div v-bind:class="{ active: item.tabKey == activeKey }" v-on:click="switchTab(item.tabKey)" class="tab-tab" v-for="item in items">{{item.tab}}</div>
	  </div>
    <div class="tab-content-container" ref="tabContainer">
      <div @touchstart="start" @mousedown="start" @touchmove="move" @mousemove="move" @touchend.stop="end" @mouseup.stop="end" class="tab-content" v-bind:style="tabContentStyle" ref="tabContent">
	      <slot></slot>
      </div>
    </div>
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
      activeKey: this.defaultActiveKey,
      sliderListWidth: '',
      tabBarStyle: {},
      tabContentStyle: {},
      preTranslateX: 0
    }
  },
  mounted () {
    console.log(this.$children)
    this.items = this.$children
    this.sliderListWidth = parseInt(this.$refs.tabContainer.offsetWidth)
    var itemCount = parseInt(this.$children.length)
    this.setTabBarStyle(itemCount)
    this.setTabContentStyle(itemCount)
    document.addEventListener('mouseup', this.end, false)
    document.addEventListener('touchend', this.end, false)
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
      this.end(null, key)
    },
    setTabBarStyle (itemCount) {
      this.tabBarStyle.top = 0
      this.tabBarStyle.left = 0
      this.tabBarStyle.right = 100 - 100 / itemCount + '%'
      this.tabBarStyle.transform = 'translate3d(0,0,0)'
    },
    setTabContentStyle (itemCount) {
      this.tabContentStyle.width = this.sliderListWidth * itemCount + 'px'
    },
    start ($event) {
      this.clientX = event.clientX
    },
    move ($event) {
      if (!this.clientX) {
        return
      }
      var moveX = event.clientX - this.clientX + this.preTranslateX
      this.tabContentStyle = Object.assign({}, this.tabContentStyle, {transform: 'translate3d(' + moveX + 'px,0,0)'})
    },
    end ($event, key) {
      console.log(key)
      var currTranslateX = 0
      if (key) {
        currTranslateX = this.sliderListWidth * -(key - 1)
      } else {
        if (!this.clientX) {
          return
        }
        if (event.clientX - this.clientX > this.sliderListWidth / 3) {
          if (parseInt(this.activeKey) > 1) {
            this.activeKey = parseInt(this.activeKey) - 1
            this.tabBarStyle.transform = 'translate3d(' + (this.activeKey - 1) * 100 + '%,0,0)'
            currTranslateX = this.sliderListWidth * -(this.activeKey - 1)
          } else {
            currTranslateX = 0
          }
        } else if (event.clientX - this.clientX < -this.sliderListWidth / 3) {
          if (parseInt(this.activeKey) < this.items.length) {
            this.activeKey = parseInt(this.activeKey) + 1
            this.tabBarStyle.transform = 'translate3d(' + (this.activeKey - 1) * 100 + '%,0,0)'
          }
          currTranslateX = this.sliderListWidth * -(parseInt(this.activeKey) - 1)
        } else {
          currTranslateX = this.preTranslateX
        }
      }
      this.tabContentStyle = Object.assign({}, this.tabContentStyle, {transform: 'translate3d(' + currTranslateX + 'px,0,0)'})
      this.clientX = ''
      this.preTranslateX = currTranslateX
      console.log('结束滑动')
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
  .tab-content-container{
    overflow: hidden;
  }
  .tab-content{
    overflow: hidden;
    user-select: none;
    position: relative;
    transition: transform 500ms ease-out;
  }
</style>
