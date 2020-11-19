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

```javascript
<script>
  export default {
    data() {
      return {
        brandname: 'payoo',
        lastname: 'pawin',
        age: 30,
        colors: ['red', 'gree', 'blug']
      }
    }
  }
</script>
```