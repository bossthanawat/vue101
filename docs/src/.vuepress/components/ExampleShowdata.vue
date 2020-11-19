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
