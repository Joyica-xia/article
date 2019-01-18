# vuex 的简单理解

## 背景

### 什么是 vuex

vuex 是一种状态管理模式，或者说我们可以称其为数据中心。

### 为什么使用 vuex

这就相当于一个集团，集团下有很多下属公司。下属公司大了之后，有些事务可能是需要集团总部集中处理，以便提高效率，降低人员冗余。vuex 就是相当于这个中央数据处理部门。我们可以把 vuex 看做总部集团保存的各下属公司都可能用到的数据。

### 何时使用 vuex

相对于本地组件直接调用数据而言，vuex 操作更加复杂，而且也意味着额外的一些开销。

#### vuex 的替代方案

- props
- provide/inject
- Portals/ Portal-Vue
  参照以下文档:
  ![何时使用vuex](https://i.imgur.com/1dvo9IK.png)

## 安装 vuex

`npm install vuex --save`

## 建立一个 vuex

1. 在入口文件`main.js`中引入并使用

```
import Vuex from 'vuex'
Vue.use(Vuex)
```

2. 按照 vuex 的模式建立一个文件
   文件:`src/store/store.js`

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

3. 将 store 文件挂载在 vue 实例下

```
new Vue({
  store,
  el: '#app',
  router,
  components: { App },
  template: '<App/>'
})
```

## vuex 中的四个概念

> vuex 中有四个概念：state、mutations、getters、actions。我们可以想象为这是总公司管理公共数据的一个部门，这个部门执行的严格管理的策略。state,代表的是这个部门管理的公共数据;mutations:对内事务管理部，修改 state，由 mutations 执行，也就是时候，要修改 state，必须经过 mutations；getters:对外输送数据部门，只输送数据，不进行其他操作;actions,中心事件,可存储中心事件，也可调用内部事件，也就是说，要进行内部事件的调用，必须由 actions 对接。

### state

存储一个中心数据

```
const state = {
  count:0
};
```

### mutations

修改一个中心数据

```
const mutations = {
	add(){
		++ state.count;
	}
}
```

### getters

向模板返回一个中心数据，类似于 computed
格式:

```
const getters = {
  DataName(state) {
    return state.DataName;
  }
};
```

举例:

```
const getters = {
  count(state) {
    return state.count;
  }
};
```

### actions

编写一个内部事件

```
const actions = {
  alertOne () {
    alert('1');
  }
};
```

调用内部事件并向模板返回，通过`commit`通行证
格式

```
const actions = {
  actionName({ commit }) {
    commit([mutationName]);
  }
};
```

```
const actions = {
  add ({ commit }) {
    commit('addAge');
  }
};
```

### 子部门和中心部门通信

我们通过对外的部门获得 vuex 存储的中心数据和操作中心事件

1. 在 componnets 文件中导入

```
import { mapGetters } from 'vuex';
computed: mapGetters(['person'])
```

2. 在 computed 中返回中心数据，在 methods 中返回中心事件

```
methods: {...mapActions(['add'])},
computed: {...mapGetters(['count'])}
```

3. 在模板中调用

```
计数:{{count}}
<input type="button" value="增加" @click="add">
```

2. 总结

- 获取中心数据:Module --> Getters --> State
- 操作中心数据:Module --> Actions --> Mutations --> State

## vuex 实例

### 计数器

- 工具:npm/cnpm/nodejs,
- 此处为 cnpm 安装 cnpm `npm install -g cnpm --registry=https://registry.npm.taobao.org

1. 安装 vue-cli
   `cnpm install vue-cli -g`
2. 利用 webpack 生成一个 vue 项目，名称为 vuex-test
   `vue init webpack vuex-test`
3. 进入 vuex-test 并运行查看

```
cd vuex-test
cnpm run dev
```

4. 安装 vuex 并在入口文件 main.js 中引入

```
//  命令行
npm install vuex --save

//  main.js
import Vuex from 'vuex'
Vue.use(Vuex)
```

5. 新建一个`vuex-test/src/store/index.js`文件
6. 根据 store 模板写入 index.js 文件

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

7. 在`main.js`中引入并将其挂载在 vuex 下

```
import store from './store/index'
new Vue({
  store,
  el: '#app',
  router,
  components: { App },
  template: '<App/>'
})
```

8. 在`store.js`中声明一个数据`count`,并为其写一个内部操作事件和外部调用事件

```
//  声明count
const state = {
  count: 0
}
//  内部操作事件
addCount (state, n) {
    let addNum = parseInt(n)
    state.count += addNum
  }
// 外部调用事件
const actions = {
  addCount ({ commit }, addNum) {
    commit('addCount', addNum)
  }
}
```

9. 新建`src/components/add-count.vue`
10. 在`add-count`文件中写入以下内容

```
<template>
  <div class="hello">
    请输入一个数:<input type="text"
      v-model="addNum"><button @click="addCount(addNum)">增加</button>
  </div>
</template>

<script>
import { mapActions } from 'vuex';
export default {
  name: 'HelloWorld',
  data () {
    return {
      addNum: null
    }
  },
  methods: {
    ...mapActions(['addCount'])
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>

```

11. 在`HelloWorld`文件中调用`add-count.vue`文件。
    写入以下内容

```
<template>
  <div class="hello">
    <add-count></add-count>
    总数:{{count}}
  </div>
</template>

<script>
import { mapGetters } from 'vuex';
import AddCount from './add-count';
export default {
  components: {
    AddCount
  },
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  computed: { ...mapGetters(['count']) }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
```

12. 效果
![addCount](https://i.imgur.com/gHF9WZj.gif)
## 参考

[1][vuex 是什么？ | vuex](https://vuex.vuejs.org/zh/)
[2][should i store this data in vuex? - markus oberlehner](https://markus.oberlehner.net/blog/should-i-store-this-data-in-vuex/)

2019/1/18 15:10:12 
