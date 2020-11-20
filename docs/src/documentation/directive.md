# Directives
ในทีนี้จะขอยกแค่เฉพาะตัวที่ใช้บ่อยๆ หากอยากรู้เพิ่มเติม อ่านได้ที่[Directives](https://vuejs.org/v2/api/?#Directives)
## v-if v-else
เลือกว่าจะแสดง หรือไม่แสดง element ที่กำหนดหรือไม่ 
> โดยจะเป็นการสร้างไหม่ หรือ ลบทิ้ง หากตรงหรือไม่ตรง case ที่เช็ค จะไม่ใช่การสร้างทิ้งไว้แล้วเลือกที่จะซ่อนหรือไม่ซ่อน element นั้นๆ แต่ถ้าแค่ต้องการซ่อนให้ใช้ [v-show](https://vuejs.org/v2/api/?#v-show) [v-if vs v-show](https://vuejs.org/v2/guide/conditional.html#v-if-vs-v-show)

>" ```v-if``` ยืดหยุ่นกว่า เพราะทำการ render ใหม่ในทุกๆครั้ง แต่ถ้าข้อมูลมีเยอะ ก็ช้ากว่า
```v-show``` เร็วกว่า เพราะไม่ต้อง render ใหม่ทุกรอบ แต่ไม่ค่อยยืดหยุ่น เพราะใช้เทคนิคปิดการแสดงผลโดยใช้ css ซึ่งถ้ามีเยอะๆ บางทีอาจจะทำให้สับสน อีกอย่าง ไม่ค่อยปลอดภัย เพราะ ข้อมูลมันถูก render มาแล้ว แค่ใช้ css ปิดไว้ " [@njth](https://medium.com/@njth/%E0%B8%AB%E0%B8%B1%E0%B8%94%E0%B9%80%E0%B8%82%E0%B8%B5%E0%B8%A2%E0%B8%99-vue-js-%E0%B9%80%E0%B8%A5%E0%B9%88%E0%B8%99%E0%B9%86-ep-1-6e476d4b260b)

> ```v-else-if``` ก็มีนะ

```html
<template>
  <div>
    ...
    <p>price: {{ price }}</p>
    <p v-if="price > 300">แพง</p>
    <p v-else>ถูก</p>
    ...
  </div>
</template>

<script>
  export default {
    data() {
      return {
        ...
        price: 300,
    }
  }
}
</script>
```
แสดงผล
<ExampleShowdata :case="4"/>


## v-on
ใช้สำหรับดักจับ event ต่างๆที่เกิดขึ้นเพื่อเรียกใช้ methods หรือ logic บางอย่าง 

เช่น ดักการ click element นั้นใช้ ```v-on:click```
::: tip
สามารถเขียน ```v-on:click``` แบบย่อได้เป็น ```@click```
:::

```html
<template>
  <div>
    ...
    <p>price: {{ price }}</p>
    ...
    <button v-on:click="increasePrice">Increase Price</button>
    <button @click="decreasePrice">Decrease Price</button>
    ...
  </div>
</template>

<script>
  export default {
    data() {
      return {
        ...
        price: 300,
    }
  },
   methods: {
    increasePrice() {
      this.price++;
    },
    decreasePrice() {
      this.price--;
    },
  },
}
</script>
```

แสดงผล
<ExampleShowdata :case="5"/>

อีกสักตัวอย่าง case ที่มีการ return output จาก event ด้วย
```html
<template>
  <div>
    <input @input="convertToUpper" type="text" placeholder="input text"/>
    <p>textUpper : {{text}}</p>
  </div>
</template>

<script>
export default {
  data(){
    return:{
      text:''
    }
  }
  methods: {
    convertToUpper(event) {
      this.text = event.target.value.toUpperCase() //ค่าของ'event'นั้นแล้วแต่ที่ event จะคืนมา ในที่นี้ <input @input=""> นั้นคืนมาเป็น object 
    }
  },
}
</script>
```

แสดงผล
<ExampleShowdata :case="5.5"/>

## v-for
ใช้สำหรับวนสร้าง element ซ้ำๆ

```html
<template>
  <div>
    ...
    <p>colors:
      <ul>
        <li v-for="color in colors">{{ color }}</li>
      </ul>
    </p>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        ...
        colors: ['red', 'green', 'yellow']
    }
  }
}
</script>
```
```v-for``` จะนำ ```colors``` ที่เป็น ```array```
```html
<!-- ผลลัพธ์หลังจาก v-for จะเหมือนเราเขียนแบบถึกๆ หน้าตาประมาณนี้ -->
<p>colors:
  <ul>
    <li>red</li>
    <li>green</li>
    <li>yellow</li>
  </ul>
</p>
```

แสดงผล
<ExampleShowdata :case="6"/>

## v-bind
ผูก property ของ tag element เข้ากับ data หรือ methods โดยใช้สัญลักษณ์ ```:``` นำหน้า

เช่น property src ของ ```<img>``` ปกติเราจะเขียน

```html
<template>
  <p><img src="https://v1.vuepress.vuejs.org/hero.png"/></p>
</template>
```

ถ้าจะเปลี่ยน String link img ของเราไปไว้ใน data property แล้วให้ src นั้นใช้ variable จาก data 

```html
<template>
  <p><img :src="imageVue"/></p>
</template>

<script>
  data() { 
      return {
        imageVue: 'https://v1.vuepress.vuejs.org/hero.png'
      }
    },
</script>
```

> ถ้ายังไม่ค่อยเข้าใจ ลอง ```<p><img :src="imageVue"/></p>``` แล้วลบ ```:``` หน้า src ดู