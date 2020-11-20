# Vue Instance (Basic)

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

## Data
คือค่า variable ที่เราสามารถนำไปใช้
```javascript
<script>
  export default {
    data() {
      return {
        weapon: 'knife',
        series: 'Z',
        price: 300,
        colors: ['red', 'green', 'yellow']
      }
    }
  }
</script>
```
เราสามารถใช้ ```{{}}``` สำหรับการนำ data variable ไปใส่ได้ 

```html
<template>
  <div>
    <p>weapon: {{ weapon }}</p>
    <p>series: {{ series }}</p>
    <p>price: {{ price }}</p>
    <p>colors: {{ colors }}</p>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        weapon: 'knife',
        series: 'Z',
        price: 300,
        colors: ['red', 'green', 'yellow']
    }
  }
}
</script>
```
แสดงผล

<ExampleShowdata :case="1"/>


::: tip 
ภายใต้ ```{{}}```สามารถเขียนพวก check true false แบบง่ายๆ เช่น {{ ```price > 300 ?'แพงจัง':'ถูกมาก'``` }}
:::

## Computed
ใช้ในเวลาที่เราต้องการคำนวณค่า data ก่อนนำไปใช้อีกทีนึง โดยที่ Computed property จะเป็น method ที่ไม่มี argument
ตัว Computed property จะอัพเดตให้เองเองเมื่อข้อมูลที่สนใจมีการเปลี่ยนแปลง หรือจะเรียกมันว่า getter method ก็ว่าได้

```html
<template>
  <div>
    <p>fullname: {{ fullname }}</p>
    <p>price: {{ price }}</p>
    <p>eventPrice: {{ eventPrice }}</p>
    <p>colors: {{ colors }}</p>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        weapon: 'knife',
        series: 'Z',
        price: 300,
        colors: ['red', 'green', 'yellow']
      },
    },
    computed: {
      fullname() {
        return this.weapon + ' ' + this.series
      },
      eventPrice() {
        if(this.price > 299) return this.price * 2
        else return this.price
      }
    }
  }
</script>
```
แสดงผล
<ExampleShowdata :case="2"/>

## Methods
เป็นส่วนสำหรับเขียน methods เพื่อเอาไปใช้

```html
<template>
  <div>
    ...
    <p>price: {{ price }}</p>
    ...
    <button @click="increasePrice">Increase Price</button>
    <button @click="decreasePrice">Decrease Price</button>
  </div>
</template>
<script>
  export default {
    ...
    methods: {
      increasePrice() {
        this.price++
      },
      decreasePrice() {
        this.price--
      }
    }
  }
</script>
```
> @click="..." ใช้สำหรับดักจับ event ต่างๆ อยู่ในหัวข้อ Directive v-on

แสดงผล
<ExampleShowdata :case="3"/>

## Watch
เป็นตัวช่วย trigger data ถ้ามีการเปลี่ยนแปลงเกิดขึ้น

```html
<script>
  export default {
    ...
    watch: {
      price(val, oldVal) {
        console.log("price : " + val, "|", "oldPrice : " + oldVal);; //จะlog ทุกครั้งที price มีการเปลี่ยนแปลง
      }
    }
  }
</script>
```
> ถ้าใช้ chrome browser ให้กด F12 ดูที่ tab "Console" เราจะเห็น log จาก console.log ที่นั้น
> เรายังสามารถ log ลง Console ได้ด้วยรูปแบบอื่นๆได้อีก [ว่าด้วยเรื่อง Consoleใน JavaScript](https://medium.com/devnote/%E0%B8%A7%E0%B9%88%E0%B8%B2%E0%B8%94%E0%B9%89%E0%B8%A7%E0%B8%A2%E0%B9%80%E0%B8%A3%E0%B8%B7%E0%B9%88%E0%B8%AD%E0%B8%87-console-log-javascript-c48b39b50ab5)

## Vue Life Cycle
ใน Life ของ Vue Instance จะมีจังหวะ hook ต่างๆ ให้เราสามารถเข้าไปแทรกจังหวะได้
- beforeCreate
- created
- beforeMount
- mounted
- beforeUpdate
- updated
- beforeDestroy
- destoryed

อ่านเพิ่มเติมแต่ละ hook แบบภาษาไทย [Life Cycle คืออะไร ?](https://medium.com/@njth/%E0%B8%AB%E0%B8%B1%E0%B8%94%E0%B9%80%E0%B8%82%E0%B8%B5%E0%B8%A2%E0%B8%99-vue-js-%E0%B9%80%E0%B8%A5%E0%B9%88%E0%B8%99%E0%B9%86-ep-2-90146f2343c9)

```html
<script>
  export default {
    ...
    created() {
      console.log('created')
      //Ex. get api เพื่อเอาข้อมูลมาใช้ หรือโชว์ จังหวะเริ่มสร้าง component นี้
    },
    mounted() {
      console.log('mounted')
    }
    ...
  }
</script>
```

## Components

ช่วยให้เราสามารถสร้าง Vue Instance ตัวอื่นๆ แล้วนำมาใช้ร่วมกันได้ 

```html
<!-- file headerWord.vue -->
<template>
  <div>
    <p>Header Word!</p>
  </div>
</template>
```

เรียกใช้ component ```headerWord.vue``` ใน ```contentWord.vue``` อีกไฟล์

```html
<!-- file contentWord.vue -->
<script>
  import HeaderWord from './headerWord.vue'
  export default {
    components: {
      HeaderWord
    }
  }
</script>
```

นำ ```HeaderWord``` มาใช้

```html
<!-- file contentWord.vue -->
<template>
  <div>
    <HeaderWord></HeaderWord>
    <!-- หรือเขียนแบบนี้ก็ได้ (แนะนำ)
    <header-word></header-word> 
    -->
    <p>Content Word!</p>
    ...
  </div>
</template>
```

แสดงผล ของไฟล์ ```contentWord.vue```

<p>Header Word!</p>
<p>Content Word!</p>