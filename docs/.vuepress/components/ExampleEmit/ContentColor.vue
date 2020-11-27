<template>
  <div>
    <app-create @createColor="addColor"></app-create>
    <!-- ใช้ v-on รับ 'createColor' event emit ที่ประกาศไว้ในตัว AppCreate และต้องรับด้วย methods เท่านั้น -->
    {{ colors }}
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