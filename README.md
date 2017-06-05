# vue-project

> A Vue.js project

```
<Tabs defaultActiveKey="1">
  <TabPane tab="tab 1" tabKey="1">
    tab1
  </TabPane>
  <TabPane tab="tab 2" tabKey="2">
    tab2
  </TabPane>
  <TabPane tab="tab 3" tabKey="3">
    tab3
  </TabPane>
</Tabs>
```

## 单文件组件里使用全局组件

```
import Vue from 'vue'
Vue.component('myComponent', {
  template: '<div>A custom component!</div>'
})
```

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report

# run unit tests
npm run unit

# run e2e tests
npm run e2e

# run all tests
npm test
```

For detailed explanation on how things work, checkout the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
