<template>
  <div>
    <div v-if="this.case == 1">
      <p>weapon: {{ weapon }}</p>
      <p>series: {{ series }}</p>
      <p>price: {{ price }}</p>
      <p>colors: {{ colors }}</p>
    </div>

    <div v-if="this.case == 2">
      <p>fullname: {{ fullname }}</p>
      <p>price: {{ price }}</p>
      <p>eventPrice: {{ eventPrice }}</p>
      <p>colors: {{ colors }}</p>
    </div>

    <div v-if="this.case == 3">
      <p>fullname: {{ fullname }}</p>
      <p>price: {{ price }}</p>
      <p>eventPrice: {{ eventPrice }}</p>
      <p>colors: {{ colors }}</p>
      <button @click="increasePrice">Increase Price</button>
      <button @click="decreasePrice">Decrease Price</button>
    </div>

    <div v-if="this.case === 4">
      <p>price: {{ price }}</p>
      <p v-if="price > 300">แพง</p>
      <p v-else>ถูก</p>
    </div>

    <div v-if="this.case === 5">
      <p>price: {{ price }}</p>
      <p v-if="price > 300">แพง</p>
      <p v-else>ถูก</p>
      <button @click="increasePrice">Increase Price</button>
      <button @click="decreasePrice">Decrease Price</button>
    </div>

    
    <div v-if="this.case === 5.5">
      <input @input="convertToUpper" type="text" placeholder="input text"/>
      <p>textUpper : {{text}}</p>
    </div>

    <div v-if="this.case === 6">
      <p>colors:
        <ul>
          <li v-for="color in colors">{{ color }}</li>
        </ul>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      weapon: "knife",
      series: "Z",
      price: 300,
      colors: ["red", "green", "yellow"],
      text:''
    };
  },
  computed: {
    fullname() {
      return this.weapon + " " + this.series;
    },
    eventPrice() {
      if (this.price > 299) return this.price * 2;
      else return this.price;
    },
  },
  props: {
    case: {
      default: 1,
    },
  },
  methods: {
    increasePrice() {
      this.price++;
    },
    decreasePrice() {
      this.price--;
    },
    convertToUpper(event) {
      this.text = event.target.value.toUpperCase();
    },
  },
  watch: {
    price(val, oldVal) {
      console.log("price : " + val, "|", "oldPrice : " + oldVal);
    },
  },
};
</script>
