<template>
  <div id="app">
	<Tabs defaultActiveKey="1">
		<TabPane tab="tab 1" tabKey="1">tab1</TabPane>
		<TabPane tab="tab 2" tabKey="2">tab2</TabPane>
		<TabPane tab="tab 3" tabKey="3">tab3</TabPane>
	</Tabs>
  </div>
</template>

<script>
import Tabs from './components/Tabs'
import TabPane from './components/TabPane'
export default {
  name: 'app',
  components: {
    Tabs, TabPane
  }
}
</script>

<style>
#app {
  
}
</style>
