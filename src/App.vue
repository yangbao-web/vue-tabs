<template>
  <div id="app">
	<Tabs defaultActiveKey="1">
		<TabPane tab="tab 1" tabKey="1">
          <CustomInput ref="customInput"/>
          <button @click="getDate">获取值</button>
        </TabPane>
		<TabPane tab="tab 2" tabKey="2">
          <my-component></my-component>
        </TabPane>
		<TabPane tab="tab 3" tabKey="3">tab3</TabPane>
	</Tabs>
  </div>
</template>

<script>
import Vue from 'vue'
Vue.component('myComponent', {
  template: '<div>A custom component!</div>'
})
import Tabs from './components/Tabs'
import TabPane from './components/TabPane'
import CustomInput from './components/CustomInput'
export default {
  name: 'app',
  components: {
    Tabs, TabPane, CustomInput
  },
  methods: {
    getDate () {
      console.log(this.$refs.customInput.getDate())
    }
  }
}
</script>

<style>
#app {
  
}
</style>
