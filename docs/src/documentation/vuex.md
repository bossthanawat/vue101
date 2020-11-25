# Vuex
[Vuex](https://vuex.vuejs.org/) คือ state management pattern + library สำหรับ Vue ทำหน้าที่เก็บข้อมูลส่วนกลางข้อมูลต่างๆ ในแอปพลิเคชั่นโดยมีกฎที่ทำให้มั่นใจได้ว่าข้อมูลสามารถเปลี่ยนแปลงได้ตามแบบที่คาดเดาได้เท่านั้น ให้เราเรียกใช้ และเข้าถึงมันได้ง่าย โดย Vuex นี้ยังถูก integrate เข้ากับ [Vue Devtool](https://github.com/vuejs/vue-devtools) เพื่อ debug และให้เราสามารถเข้าไปดู state ต่างๆ ได้ง่าย

## Installation
> ถ้า Create ด้วย vue cli (command create project: vue create xxx) เราสามารถเลือกให้ติดตั้ง vuex ให้ได้เลย CLI จะทำการ set แล้วสร้างไฟล์ตัวอย่างให้เรียบร้อยทันที ไม่ต้อง installation เอง

กรณี install เอง
```bash
npm install vuex --save
# or
yarn add vuex
```
เพิ่ม Vuex ในแอปพลิเคชันของคุณ เมื่อใช้กับ module system คุณต้องติดตั้ง Vuex ผ่าน ```Vue.use()```

```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)
export default new Vuex.Store({
  ...
})
```
ที่ main.js
```js
new Vue({
  store, // <----- import store
  render: h => h(App)
}).$mount('#app')
```


## Getting Started

Create Project ด้วย Vue CLI แล้วให้เลือก install vuex 

หลังจาก Create เรียบร้อยแล้วให้ลองดูที่  ```/src/main.js``` มีการกำหนด store ให้ตั้งแต่ตอนสร้าง Vue instance โดยใช้ค่าที่ export มาจาก ```/src/store```

```js
import Vue from 'vue'
import App from './App.vue'
import router from './router'
import store from './store'

Vue.config.productionTip = false

new Vue({
  router,
  store,
  render: h => h(App)
}).$mount('#app')
```
ดูที่ไฟล์ ```/src/store.js``` จะเห็นว่ามีการ export Vuex.Store ออกไป พร้อมกับการกำหนด property ต่างๆ ใน Vuex ได้แก่ state, mutations, actions, getter รวมถึง modules

```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {
  },
  mutations: {
  },
  actions: {
  },
  modules: {
  }
})

```

## Core Concepts
> *ตัวอย่างบางส่วนเอามาจาก [khomkrit](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#Vuex) [vuex](https://vuex.vuejs.org/guide)*

### State
> Vuex uses a single state tree - that is, this single object contains all your application level state and serves as the "single source of truth." This also means usually you will have only one store for each application. A single state tree makes it straightforward to locate a specific piece of state, and allows us to easily take snapshots of the current app state for debugging purposes.

```js
// file store/index.js
state: {
  items: ['foo','bar']
}
```
#### Getting Vuex State into Vue Components

เราสามารถอ้างถึงค่านี้ได้ใน Components โดยใช้ ```this.$store```

```html
<template>
  <div>{{ items }}<div>
</template>
<script>
  ...
  computed: {
    items () {
      return this.$store.state.items
    }
  },
  // ไม่แนะนำให้แก้ค่าที่ state โดยตรง ให้ทำผ่าน Mutations,Actions
  methods: {
    addTodo() {
      this.$store.state.items.push('bee')
    }
  }
</script>

```
อธิบายแบบง่ายๆก็คือย้ายการเก็บ data ใน component ไปไว้ที่ state ตรงกลางใน vuex นั้นเอง

#### The mapState Helper
โดยปกติแล้วเราจะไม่อ้างถึง this.$store ตรงๆ แต่จะใช้ผ่าน map helper แทน

```js
import { mapState } from "vuex";

computed: {
  ...mapState({
    items : state => state.items, // this.$store.state.items
    // passing the string value 'items' is same as `state => state.items`
    items : 'items', 
    // ...
  })
}
```

### Mutations
> The only way to actually change state in a Vuex store is by committing a mutation. [Mutations](https://vuex.vuejs.org/guide/mutations.html#commit-with-payload)

วิธีเดียวที่เราจะเปลี่ยนค่า state นั้นจะต้องใช้ mutation

อธิบายง่ายๆ ตัว mutations ก็เปรียบเสมือนตัว setState นั้นเอง


> กฏเหล็กข้อหนึ่งของ mutations ก็คือ mutation handler functions จะต้องเป็น ```synchronous``` เท่านั้น [mutations-must-be-synchronous](https://vuex.vuejs.org/guide/mutations.html#mutations-must-be-synchronous)

จากตัวอย่างที่เขียนไว้ที่ state เกี่ยวกับ logic เราจะย้ายที่ไป Mutations แทน
```js
// old code
  methods: {
    addTodo() {
      this.$store.state.items.push('bee')
    }
  }
```

```js
// new code move logic to file vuex
// file store/index.js
mutations: {
  'ADD_ITEM' (state, payload) {
    state.items.push(payload.item)
  }
}
```
เราจะมี ```mutation``` ชื่อว่า ```ADD_ITEM``` ใช้สำหรับ add ข้อมูลเข้า ```items```

```js
addTodo() {
  this.$store.commit('ADD_ITEM', { item: 'bee'})
},
```
#### The mapMutations Helper
สามารถใช้ ```mapMutations``` แทน ```this.$store.comit```
```js
methods: {
  ...mapMutations([
    addItem : 'ADD_ITEM' //import commit function name 'ADD_ITEM'
  ]),
  addTodo() {
    this.addItem({ item: 'bee'}) // เรียกใช้ 'ADD_ITEM' เพื่อ Add 'bee' เข้า state.items
  }
}
```
### Actions

คล้ายกับ mutations แต่สิ่งที่ต่างออกไปก็คือ

- แทนที่จะแก้ไข data ที่ state ตรงๆ ก็จะใช้วิธี commit mutation แทนอีกทีนึง
- โค้ดใน action สามารถเป็น ```aynschronous``` ได้

ใน action จะมีการรับ payload เข้ามาแล้วใช้ commit mutation อีกที นึง

```js
actions: {
  addItem({ commit }, payload) {
    commit('ADD_ITEM', payload) // commit mutations ที่ชื่อ ADD_ITEM 
  }
}
```

ตอนเรียกใช้ใน App
```js
methods: {
  addTodo() {
    this.$store.dispatch('addItem', { item: this.item })
    // จะเรียก action 'addItem' ซึ่ง action นี้ก็จะไป commit เพื่อ add item ลง state.item อีกทีนึง
  }
}
```
#### The mapActions Helper
สามารถใช้ ```mapActions``` แทน ```this.$store.dispatch```

```js
methods: {
   ...mapActions({
     addItem : 'addItem'
   }),
  addTodo() {
    this.addItem({ item: 'bee'})
  }
}
```
::: details Example Composing Actions
```js
actions: {
  actionA ({ commit }) {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        commit('someMutation')
        resolve()
      }, 1000)
    })
  }
}
```
```js
// assuming `getData()` and `getOtherData()` return Promises

actions: {
  async actionA ({ commit }) {
    commit('gotData', await getData())
  },
  async actionB ({ dispatch, commit }) {
    await dispatch('actionA') // wait for `actionA` to finish
    commit('gotOtherData', await getOtherData())
  }
}
```
:::


### Getters
### Modules

