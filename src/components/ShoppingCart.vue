<template>
  <div v-on:changeQuantity="alert('')">
    <h1>Shopping Cart</h1>
    <ul>
      <li v-for="p in products" v-bind:key="p.id">
        <input type="checkbox" v-model="p.checked">
        {{ p.title }} | {{ p.quantity }} | {{ p.price | formatMoney }} | {{ p.quantity * p.price | formatMoney }}
        <QuantityButton v-on:changeQuantity="changeQuantity" v-bind:id="p.id"/>
      </li>
    </ul>
    <div>
      <button v-on:click="checkAll">Check All</button>
      <button v-on:click="uncheckAll">Uncheck All</button>
      {{totalAmount | formatMoney}}
    </div>
  </div>
</template>

<script>
import QuantityButton from "./QuantityButton";
export default {
  components: {
    QuantityButton
  },
  data() {
    return {
      products: [
        {
          id: 0,
          title: "Product AAA",
          quantity: 1,
          price: 13.99,
          checked: true
        },
        {
          id: 1,
          title: "Product BBB",
          quantity: 5,
          price: 13.99,
          checked: false
        },
        {
          id: 2,
          title: "Product CCC",
          quantity: 5,
          price: 13.99,
          checked: true
        }
      ]
    };
  },
  filters: {
    formatMoney(value) {
      return "¥" + value.toFixed(2);
    }
  },
  methods: {
    changeQuantity: function(id, amount) {
      this.products[id].quantity += amount;
    },
    checkAll: function() {
      this.products.forEach(function(item, index) {
        item.checked = true;
      });
    },
    uncheckAll: function() {
      this.products.forEach(function(item, index) {
        item.checked = false;
      });
    }
  },
  computed: {
    totalAmount: function() {
      let total = 0;
      this.products.forEach(function(item, index) {
        if (item.checked) {
          total += item.quantity * item.price;
        }
      });
      return total;
    }
  }
};
</script>

<style scoped>
li {
  list-style: none;
}
</style>

