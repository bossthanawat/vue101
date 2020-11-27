# Instant Prototype

การเขียน ```vue``` เราจะใช้ไฟล์ ```*.vue``` ซึ่งเป็น  Vue Instance ที่จะถูกเรียกใช้โดย Vue runtime ในการทำงาน โดยในไฟล์ ```*.vue``` จะประกอบไปด้วย 3 ส่วนหลัก ที่อยู่ในลักษณะของ Tag HTML

- ## template
เป็นส่วนสำหรับใส่เนื้อหาที่ต้องการแสดงในหน้าเว็บ เป็นส่วนสำหรับเขียน Tag HTML เป็นหลัก

```html
<template>
  <div>Hello World!</div>
</template>
```

- ## script
เป็นส่วนสำหรับเขียน script ต่างๆ ของแอป และส่วนของที่ต้องการควบคุมเนื้อหาใน ```<template></template>```

```javascript
<script>
  import Hi from 'ntt';
  const test ='Hi'
  export default {
    ...
  }
</script>
```

- ## style
พื้นที่สำหรับเขียน style เช่น css เพือนำไปใช้ใน ```<template></template>```

```javascript
<style>
  .bodyMan {
    font-size: 14px;
  }
<style>
```

หน้าตาของเจ้าไฟล์ ```.vue``` ก็จะประมาณนี้

```javascript
<template>
  <div class="bodyMan">Hello World!</div>
</template>

<script>
  //...  
</script>

<style>
  .bodyMan {
    font-size: 14px;
  }
<style>
```

<p class="codepen" data-height="400" data-theme-id="dark" data-default-tab="js,result" data-user="thanawat" data-slug-hash="BazXeoe" style="height: 400px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="vue101">
  <span>See the Pen <a href="https://codepen.io/thanawat/pen/BazXeoe">
  vue101</a> by thanawat (<a href="https://codepen.io/thanawat">@thanawat</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

## vue serve
คุณสามารถสร้างต้นแบบได้อย่างรวดเร็วด้วยไฟล์ ```*.vue``` แล้ว run โดยใช้คำสั่งvue serve 

พูดง่ายๆคือเป็นการ run ในโหมด dev นั้นเอง

ลองทดสอบโดยการสร้างไฟล์ ```test.vue``` โดยไฟล์นี้นั้นจะเป็น Vue Instance 1 ตัว

```html
<!-- file test.vue -->
<template>
  <h1>Hello World!</h1>
</template>
```

แล้วลอง run ด้วยคำสั่ง [vue serve](https://cli.vuejs.org/guide/prototyping.html)

```bash
vue serve test.vue
```

เราก็จะเห็นหน้าจอแสดงข้อความว่า Hello World!
::: warning 
**Every component must have a single root element.** vue นั้นจะต้องมี root element เพียงหนึ่งเดียว
:::
