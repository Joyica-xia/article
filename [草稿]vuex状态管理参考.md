# vuex状态管理参考
状态事件管理器
几种仓库
公司各有自己的数据仓库、子公司都有自己的数据仓库
数据重复，管理有成本，总公司建立一个公有仓库，要的话去提。
核心概念
state - 数据 所有的原始数据
getter - 计算属性 computed 跟我的state相关
   getter-Module关联
Mutation:内部事件，控制state, 内部管理部门
Action -事件-Moduele 外联部
Module -外部的模板xxx.vue components
Module控制Getter,Getter控制state
Module -> Getter -> State 模板(Module)必须通过getter获得数据。在js中体现在通过getter暴露数据，在template体现在通过mapGetter获取数据
	-> Action -> Mutation
[开始|vuex](https://vuex.vuejs.org/zh/guide/)
安装
`npm install vuex --save`
使用
1. 在入口文件main.js中引用并使用
```
import Vuex from 'vuex'

Vue.use(Vuex)
```
2. 在总目录下新建一个src/store/store.js文件
3. 初始化store.js文件
```
import Vue from 'vue';
import Vuex from 'vuex';

Vue.use(Vuex)

const state = {}

const getters = {}
const mutations = {}
const actions = {}
export default new Vuex.Store({
  state,
  mutations,
  actions,
  getters
})

```
4. 在入口文件main.js中声明store.js文件
```
new Vue({
  store,
  el: '#app',
  router,
  components: { App },
  template: '<App/>'
})
```

案例
1. 存储一个对外变量并暴露
在store.js中声明并暴露，类似于计算属性
```
const state = {
  person: {
    name: 'jack',
    age: 12
  }
};

const getters = {
  person (state) {
    return state.person;
  }
};
```
2. 在components中通过mapGetters获取
```
//	template
 名字:{{person.name}}
 年龄:{{person.age}}
//script
import { mapGetters } from 'vuex';
computed: mapGetters(['person'])

```
2. 获取一个中心存储事件
```
//在外联部中编写一个对外事件
const actions = {
  add () {
    alert('1');
  }
};

//template
增加年龄:<input type="button" @click="add" value="添加">
// 在scirpt中引入并使用
import { mapGetters, mapActions } from 'vuex';
methods: mapActions(['add']),
```

3. 操作中心存储数据
module--> actions --> mutations--->state
```
//	在内部管理部中新增一个事件 addAge
const mutations = {
  addAge () {
    state.person.age++;
  }
};
//	在外联部中通过commit通行证调用内部事件
const actions = {
  add ({ commit }) {
    commit('addAge');
  }
};
```

将state单独分离为文件
## 中级用法
```
 //我们可以在里面进行更加复杂的操作
```  
2019/1/17 0:41:39 
