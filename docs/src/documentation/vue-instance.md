# Vue Instance

*ขอบคุณข้อมูลส่วนใหญ่จาก https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#methods [khomkrit](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#methods)
[The Vue Instance](https://vuejs.org/v2/guide/instance.html)*

::: details Creating a Vue Instance

แอปพลิเคชัน Vue ทุกตัวเริ่มต้นด้วยการสร้างInstance Vue ด้วยVueฟังก์ชัน:

```javascript
  var vm = new Vue({
    // options
  })
```

:::

## data
คือค่า variable ที่เราสามารถนำไปใช้
```javascript
<script>
  export default {
    data() {
      return {
        brand: 'nikon',
        series: 'Z',
        price: 300,
        colors: ['red', 'gree', 'yellow']
      }
    }
  }
</script>
```
เราสามารถใช้ ```{{}}``` สำหรับการนำ data variable ไปใส่ได้ 

```html
<template>
  <div>
    <p>brand: {{ brand }}</p>
    <p>series: {{ series }}</p>
    <p>price: {{ price }}</p>
    <p>colors: {{ colors }}</p>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        brand: 'nikon',
        series: 'Z',
        price: 300,
        colors: ['red', 'gree', 'yellow']
    }
  }
}
</script>
```
แสดงผล

<ExampleShowdata/>


::: tip 
ภายใต้ ```{{}}```สามารถเขียนพวก check true false แบบง่ายๆ เช่น {{ ```price > 300 ?'แพงจัง':'ถูกมาก'``` }}
:::

