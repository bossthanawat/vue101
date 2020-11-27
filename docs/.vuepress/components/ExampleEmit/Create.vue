<template>
  <form @submit.prevent="saveColor">
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
      color: "",
    };
  },
  methods: {
    saveColor() {
      this.$emit("createColor", this.color); // ประกาศ emit event ชื่อ 'createColor' ที่ส่งค่า color
    },
  },
};
</script>