# vuex-config
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
  userInfo: {
    id:12,
    userName:'jay',
    sex: 'man',
    country: 'china',
    city: 'shanghai',
    favorite: [ 'book', 'game', 'sing']
   }
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
export const ADD_FAVORITE = 'ADD_FAVORITE'
```
#### store>mutations.js
```
import * as types from './types'
consts mutations = {
  [types.GET_USER_INFO] (state) {
    alert(state.userInfo.userName,state.userInfo.sex,state.userInfo.city)
    return state.userInfo
  },
  [types.ADD_FAVORITE] (state, newFavorite) {
    state.userInfo.favorite.push(newFavorite)
  }
}
```
#### store>actions.js
```
immport * as types from './types'
export const GET_USER_INFO = ({commit}) => commit(types.GET_USER_INFO)
export const ADD_FAVORITE = ({commit}, newFavorite) => commit(types.ADD_FAVORITE, newFavorite)
```
#### src>index.js
```
<template>
name: <p>{{userInfo.userName}}</p>
sex: <p>{{userInfo.sex}}</p>
phone: <p>{{userInfo.phone}}</p>
city: <p>{{userInfo.city}}</p>
country: <p>{{country}}</p>
<button @click="printUserInfo">弹出用户信息</button>
</template>
<script type="text/babel">
import { mapActions , mapState, mapMutations, mapGetters } from 'vuex'
export default {
  data () {
    userInfo: this.$store.state.userInfo
  },
  mounted () {},
  computed: mapStates({
    country: state => state.userInfo.country,
  }),
  methods: {
    // 第一种 (分发 dispatch)
    // ...mapActions({printUserInfo: 'GET_USER_INFO'}),
    // 第二种 (分发 commit)
    // ...mapMutations({printUserInfo: 'GET_USER_INFO'}),
    // 第三种
    printUserInfo () {
      this.$store.dispatch('GET_USER_INFO')
    }
  }
} 
```

最后附上vuex 里面几个工具函数（mapActions，mapState，mapMutations，mapGetters）的 [详细讲解](https://vuex.vuejs.org/zh-cn/state.html)
















