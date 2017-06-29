# vuex-configvue
vuex实战项目中简单实用的配置，这次主要介绍vuex的使用，欢迎 Star or Issue

#### 通常我们的项目的目录结构是这样的

```
├── README.md
├── dist  // 打包构建后的文件夹
│   ├── build.js
│   └── build.js.map
├── index.html
├── package.json
├── src
│   ├── App.vue
│   ├── assets
│   │   ├── css.css
│   │   ├── icon.css
│   │   └── logo.png
│   ├── constant
│   │   └── api.js  // 配置api接口文件
│   ├── http.js // 封装fetch、post请求及http 拦截器配置文件
│   ├── index.vue   <-------------------------------------------------------------------------------------------
│   ├── login.vue 
│   ├── main.js
│   ├── repository.vue
│   ├── router.js // 路由配置文件
│   └── store
│       ├── index.js  <-------------------------------------------------------------------------------------------
│       └── types.js   <-------------------------------------------------------------------------------------------
│       └── mutations.js  <-------------------------------------------------------------------------------------------
│       └── actions.js   <-------------------------------------------------------------------------------------------
└── webpack.config.js
```

#### store>index.js
```
import Vue from 'vue'
import Vuex from 'vuex
impor mutations from './mutations'
import * as types from './types'
import * as actions from './actions'
Vue.use(Vuex)
const state = {
  id:12,
  userName:'jay',
  sex: 'man',
  country: 'china',
  city: 'shanghai',
  favorite: [ 'book', 'game', 'sing']
}
const debug = process.env.NODE_ENV !== 'production'
const store = new Vuex.Store({
  state,
  mutations,
  actions,
  // true ，如果不是通过mutations，而直接修改state的状态会抛出错误
  strict:debug,
  // state 发生变化对应的追踪日志
  // plugins: [ debug ? ['createLogger()' : [] ]
})
```
#### store>types.js
```
export const GET_USER_INFO = 'GET_USER_INFO'
export const SET_USER_FAVORITE = 'SET_USER_FAVORITE'
```
#### store>mutations.js
```
import * as types from './types'
consts mutations = {
  [types.GET_USER_INFO] (state) {
    return state
  },
  [types.SET_USER_FAVORITE] (state, newFavorite) {
    state.favorite.push(newFavorite)
  }
}
```
#### store>actions.js
```
export const GET_USER_INFO = ({commit}) => commit('GET_USER_INFO')
export const SET_USER_FAVORITE = ({commit}, newFavorite) => commit('SET_USER_FAVORITE', newFavorite)
```
#### src>index.js
```
<template>
name:
</template>
<script type="text/babel">
import { mapActions } from 'vuex'
export default {
  data () {
  },
  mounted () {
  
  },
  methods: {
    ...mapActions({addFavorite: 'SET_USER_FAVORITE'})
  }
} 
```

















