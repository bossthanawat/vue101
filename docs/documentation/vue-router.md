# Vue Router

Vue Router เป็น official router ของ Vue เอง เป็นส่วนสำหรับการ map เส้นทาง Path ต่างๆ กำหนดพารามิเตอร์ กำหนดพฤติกรรมการเข้าถึงแต่ละเส้นทาง และอื่นๆ อ่านเพิ่มเติมได้ที่ [Vue Router](https://router.vuejs.org/)

## Getting Started

### App.vue
ที่ File ```App.vue``` (Main root) และสมมุติว่ามีไฟล์ component ย่อยๆอีกชื่อว่า ```Home.vue``` และ ```About.vue```

```html
<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link>
      <!-- or <router-link :to="{ name: 'home' }>Home</router-link> -->
      <router-link to="/about">About</router-link>
    </div>
    <router-view/>
  </div>
</template>
```

```<router-link/>``` คล้ายกับ ```<a/>``` แต่เป็น Tag สำหรับการพาไปเส้นทางอื่นๆ ที่ทำให้หน้า web ของเราไม่เกิดการโหลดหน้าใหม่ซ้ำ เพราะ Vue เป็น ```Single Page Application```

```<router-view/>``` เปรียบเสมือนเรียกใช้ Component แต่แค่เป็นการ Import เรียก Component ผ่าน router แทน


### router.js
ที่ไฟล์ JavaScript Router ```router.js``` , ```router/index.js```

```Javascript
import Vue from 'vue'
import VueRouter from 'vue-router'

import Home from '../views/Home.vue'
import about from '../views/About.vue'

Vue.use(VueRouter)

const routes = [
  {
    path: '/',
    name: 'Home',
    component: Home
  },
  {
    path: '/about',
    name: 'About',
    component: about
  }
]

const router = new VueRouter({
  mode: 'history',
  routes
})

export default router
```


เป็นพื้นที่สำหรับการเขียน config route ต่างๆ 

เช่น ที่```const routes=[...]```

key ```path``` คือชื่อ ของ path บน URL ที่เราเห็นนั้นเอง

key ```component``` คือการประกาศว่าที่ path นั้นๆต้องการให้ render component อะไร

### main.js
ที่ไฟล์ ```main.js``` import router เข้าไป

```Javascript
import Vue from 'vue'
import App from './App.vue'
import router from './router'

...

new Vue({
  router, // <--------- use router
  render: h => h(App)
}).$mount('#app')
```

## Dynamic Route Maching 
ทำให้เราสามารถกำหนด route maching โดยไม่ต้องกำหนดชื่อ path เป็นค่าคงที่

เช่น เช่นเราอาจมี User แสดงผลสำหรับผู้ใช้ที่แตกต่างกันระบุด้วย ID

```Javascript
const User = {
  template: '<div>User</div>'
}

const router = new VueRouter({
  routes: [
    // dynamic segments start with a colon
    { path: '/user/:id', component: User }
  ]
})

```

ถ้ามีคนเรียก path มาที่ /user/101 เราก็สามารถเอาค่านี้มาใช้ได้เลยจากใน Vue โดยใช้ this.$route.params

```Javascript
const User = {
  template: '<div>User {{ $route.params.id }}</div>'
}
```

อ่านเพิ่มเติม [Dynamic Route Matching](https://router.vuejs.org/guide/essentials/dynamic-matching.html#reacting-to-params-changes)

## Nested Routes

การใช้งานจริงๆเรามักจะเจอการเขียนซ้อนในซ้อนลึกลงไปหลายระดับ นอกจากนี้ยังเป็นเรื่องปกติมากที่กลุ่มของ URL จะสอดคล้องกับโครงสร้างบางส่วนของ component

```
/user/foo/profile                     /user/foo/posts
+------------------+                  +-----------------+
| User             |                  | User            |
| +--------------+ |                  | +-------------+ |
| | Profile      | |  +------------>  | | Posts       | |
| |              | |                  | |             | |
| +--------------+ |                  | +-------------+ |
+------------------+                  +-----------------+
```

เราสามารถประกาศ ```<vue-router/>``` หลายๆตัวลึกลงไปในแต่ละ component ได้

```html
<!-- file App.vue -->
<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>
```
ตอนนี้ App.vue เป็น route view กรอบนอกสุด

```html
<!-- file User.vue -->
<template>
  <div class="user">
    <h2>User {{ $route.params.id }}</h2>
    <router-view></router-view>
  </div>
</template>
```
ประกาศ ```<router-view>``` อีกชั้นนึง เปรียบเสมือนเป็นกรอบชั้นในอีกทีจาก App.vue นั้นเอง

```Javascript
// file router.js
...
const router = new VueRouter({
  routes: [
    { path: '/user/:id', component: User,
      children: [
        {
          // UserProfile will be rendered inside User's <router-view>
          // when /user/:id/profile is matched
          path: 'profile',
          component: UserProfile
        },
        {
          // UserPosts will be rendered inside User's <router-view>
          // when /user/:id/posts is matched
          path: 'posts',
          component: UserPosts
        }
      ]
    }
  ]
})
```

สุดท้ายประกาศ ```children``` ในตัว config router

จะเห็นว่า component กับ path ของ```UserProfile``` และ ```UserPosts``` อยู่ภายใต้ ```User```

สุดท้ายแล้วสมมุตติว่า มีการเรียกใช้ URL ```/user/101/profile``` ผลลัพธ์ของ html ก็จะหน้าตาประมาณนี้

```html
<div id="app"> < --- App.vue
  <div class="user"> < --- User.vue
    <h2>User 101</h2>
    <UserProfile/> < --- UserProfile.vue
  </div>
</div>
```

## Programmatic Navigation 

นอกจาก ```<router-link>``` เพื่อสร้าง tag hmtl ในการนำทางแล้ว เรายังสามารถใช้ router instance methods ได้
- router.push(...)
```Javascript
// literal string path
router.push('home')

// object
router.push({ path: 'home' })

// named route
router.push({ name: 'user', params: { userId: '123' } })
```

- router.replace(...)
- router.go(...)

[เพิ่มเติม](https://router.vuejs.org/guide/essentials/navigation.html)

## Navigation Guards

ใช้สำหรับทำบางสิ่งบางอย่าง ก่อนหรือหลังที่จะเข้ามาที่ route ได้ เช่นการตรวจสอบว่าถ้าเปิดมาที่ path นี้แล้วยังไม่ให้ login เราก็จะ redirect ไปที่หน้า login 
```Javascript
const router = new VueRouter({ ... })

router.beforeEach((to, from, next) => {
  // ...
})
```

```Javascript
router.beforeEach((to, from, next) => {
  // เช็คว่า ถ้าหน้าที่กำลังจะไปนั้น path name ไม่ใช่ Login และ ยังไม่ได้Authenticated ให้พาไปที่หน้า Login แทน
  if (to.name !== 'Login' && !isAuthenticated) next({ name: 'Login' })
  // next() คือ ให้ไปหน้าที่กำลังจะไปได้ปกติ
  else next()
})
```

## [Lazy Loading Routes](https://router.vuejs.org/guide/advanced/lazy-loading.html#grouping-components-in-the-same-chunk)
บาง component เรายังไม่อยากให้โหลดมาตั้งแต่ตอนแรก เราสามารถกำหนดได้ว่าให้โหลดมาตอนไหนในภายหลังได้ ว่าจะโหลดมาเฉพาะ component โดดๆ หรือโหลดมาพร้อมกับ component อื่นๆ

```Javascript
//basic
import Foo from './Foo.vue'

// Lazy Loading
// ลองกด F12 แล้วดูตอน web โหลดหน้า page
const Foo = () => import('./Foo.vue')
// กำหนดชื่อตอน client โหลดไปได้ หรือ group รวมได้(ตั้งชื่อให้เหมือนกัน) โดยใช้webpackChunkName 
const Foo = () => import(/* webpackChunkName: "group-foo" */ './Foo.vue')
const Bar = () => import(/* webpackChunkName: "group-foo" */ './Bar.vue')
```


Vue router ยังมีหัวข้ออื่นๆอีก อ่านเพิ่มเติมที่ [vue-router](https://router.vuejs.org/)

