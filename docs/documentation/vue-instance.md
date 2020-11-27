# Vue Instance (Basic) API 2.x

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

```html
<script>
  export default {
    ...
    created() {
      console.log('created')
      //Ex. get api เพื่อเอาข้อมูลมาใช้หรือโชว์ ก่อนที่ component จะเริ่ม render
    },
    mounted() {
      console.log('mounted')
    }
    ...
  }
</script>
```

<p class="codepen" data-height="481" data-theme-id="dark" data-default-tab="js,result" data-user="thanawat" data-slug-hash="PoGYKry" style="height: 481px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Vue lifecycle example">
  <span>See the Pen <a href="https://codepen.io/thanawat/pen/PoGYKry">
  Vue lifecycle example</a> by thanawat (<a href="https://codepen.io/thanawat">@thanawat</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>


อ่านเพิ่มเติมแต่ละ hook แบบภาษาไทย [Life Cycle คืออะไร ?](https://medium.com/@njth/%E0%B8%AB%E0%B8%B1%E0%B8%94%E0%B9%80%E0%B8%82%E0%B8%B5%E0%B8%A2%E0%B8%99-vue-js-%E0%B9%80%E0%B8%A5%E0%B9%88%E0%B8%99%E0%B9%86-ep-2-90146f2343c9)

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

## Props

เราสามารถเขียนรับค่าบางสิ่งเข้าไปใน component เพื่อนำมาใช้ได้โดยใช้ Props

เพิ่มให้ ```HeaderWord.vue``` สามารถรับค่าได้ 

```html
<!-- file headerWord.vue -->
<template>
  <div>
    <p>{{msg}}</p>
  </div>
</template>

<script>
export default {
  props: ['msg'],
  ...
}
</script>
```

โดยให้ ```contentWord.vue``` เป็นคนส่งค่าให้

```html
<!-- file contentWord.vue -->
<template>
  <div>
    <header-word msg="Props Word!"></header-word> 
    <p>Content Word!</p>
    ...
  </div>
</template>
```

แสดงผล ของไฟล์ ```contentWord.vue```

<p>Props Word!</p>
<p>Content Word!</p>

> ยังมีวิธีเขียน Props อีกหลายแบบอ่านเพิ่มเติมที่ [Props](https://vuejs.org/v2/guide/components-props.html)

## Slot
ใช้ ```<slot></slot>``` เพื่อใช้เป็นช่องทางการแจกจ่ายสำหรับเนื้อหา

ยังมี Slot อีกหลายแบบอ่านเพิ่มเติมได้ที่ [Slot](https://vuejs.org/v2/guide/components-slots.html)

เพิ่ม slot ใน ```headerWord.vue```

```html
<!-- file headerWord.vue -->
<template>
  <div>
    <slot></slot>
    <p>{{msg}}</p>
  </div>
</template>
```
ใน ```contentWord.vue``` ลองเขียน tag ภายใต้ tag ```header-word```
```html
<!-- file contentWord.vue -->
<template>
  <div>
    <header-word msg="Props Word!">
      <p>Slot Word!<p>
    </header-word> 
    <p>Content Word!</p>
    ...
  </div>
</template>
```
แสดงผล ของไฟล์ ```contentWord.vue```

<p>Slot Word!</p>
<p>Props Word!</p>
<p>Content Word!</p>

## Emit

เป็นการส่งค่าออกจาก component

ตัวอย่างจาก [khomkrit](https://www.khomkrit.com/self-studying-vuejs-in-30-minutes/#Directive)
```html
<!-- file Create.vue -->
<template>
  <form @submit.prevent="saveColor"> <!-- submit แล้วจะเรียก saveColor-->
    <div>
      <label>Input new Color</label>
      <input
        type="text"
        class="form-control"
        placeholder="input"
        v-model="color"
      />
    </div>
    <button type="submit">Submit</button>
  </form>
</template>
<script>
export default {
  data() {
    return {
      color: ''
    }
  },
  methods: {
    saveColor() {
      this.$emit('createColor', this.color) // ประกาศ emit event ชื่อ 'createColor' ที่ส่งค่า color
    }
  }
}
</script>
```

```html
<template>
  <div>
    <app-create @createColor="addColor"></app-create>
     <!-- ใช้ v-on รับ 'createColor' event emit ที่ประกาศไว้ในตัว AppCreate และต้องรับด้วย methods เท่านั้น -->
     {{colors}}
  </div>
</template>
<script>
  import Create from './Create.vue'
  export default {
    data() { 
      return {
        colors:[]
      }
    },
    methods: {
      addColor(color) {
        this.colors.push(color) 
        // ค่าของ color คือ this.color จาก AppCreate ที่ส่งมา
        // มันก็เหมือนกับเขียนรับ event @click @input เพียงแต่อันนี้เราเขียน event เอง ตั้งชื่อเอง return ค่าเอง
      }
    },
    components: {
      AppCreate: Create
    }
  }
</script>
```

แสดงผล
<ExampleEmit-ContentColor/>