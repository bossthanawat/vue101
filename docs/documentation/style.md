# Style (CSS)

พื้นที่สำหรับเขียน css เราจะเขียนไว้ภายใต้ ```<style></style>```

```html
<style>
  /*…write your styles here*/
  button {
    color: #4fc08d;
  }
</style>
```
::: warning 
css ที่ประกาศภายใต้ ```<style></style>``` จะเป็น global ทำให้ component อื่นจะสามารถถูกเรียกใช้ได้
:::

## Scoped CSS

```html
<style scoped>
  /*…write your styles here*/

</style>
```

เมื่อ ```<style>``` มี tag ```scoped``` css จะถูกใช้เพียงแค่ใน elements ของ component ในตัวมันเองเท่านั้น


## Mixing Local and Global Styles

คุณสามารเขียน local (scoped) และ global (non-scoped) ใน component เดียวกันได้

```html
<style>
/* global styles */
</style>

<style scoped>
/* local styles */
</style>
```

## Deep Selectors

ในบางครั้งหากคุณต้องการใช้ Deep ภายใต้ tag scoped คุณสามารถใช้ ```>>>```

```html
<style scoped>
.a >>> .c { /* ... */ }
/* ต้องการเขียน css ที่ .c ที่อยู่ภายใต้ .a */
/* 
<div class="a">
  <div class="b">
    <button class="c"/>
  </div>
</div>
 */
</style>
```

> Sass สามารถใช้ ```::v-deep``` แทนได้ ```>>>```


## CSS Preprocessor

เรายังสามารถเขียน css ในรูปแบบอื่นๆ เช่น scss หรือ sass ได้เพียงแค่ประกาศ tag ```lang``` 

แต่ว่า project อาจจะต้องมีการ install ตัว loader เพิ่มเติมด้วย หรือ config เพิ่มในบางกรณี [pre-processors](https://cli.vuejs.org/guide/css.html#pre-processors)

[มาทำให้การเขียน CSS ง่ายขึ้น ด้วย SASS กันเถอะ](https://konoesite.com/%E0%B8%A1%E0%B8%B2%E0%B8%97%E0%B8%B3%E0%B9%83%E0%B8%AB%E0%B9%89%E0%B8%81%E0%B8%B2%E0%B8%A3%E0%B9%80%E0%B8%82%E0%B8%B5%E0%B8%A2%E0%B8%99-css-%E0%B8%87%E0%B9%88%E0%B8%B2%E0%B8%A2%E0%B8%82%E0%B8%B6%E0%B9%89%E0%B8%99-%E0%B8%94%E0%B9%89%E0%B8%A7%E0%B8%A2-sass-%E0%B8%81%E0%B8%B1%E0%B8%99%E0%B9%80%E0%B8%96%E0%B8%AD%E0%B8%B0-ec17b2a79c6a)

```html
<style lang="scss">
/* write SCSS here */
</style>
```



