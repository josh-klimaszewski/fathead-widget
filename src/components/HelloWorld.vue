<template>
  <div>
    <h1>Shopping Cart</h1>  
    <div class="cart">
        <div class="cart-header">
          <div>Name</div>
          <div>Quantity</div>
          <div>Total</div>
        </div>
        <div class="cart-product" v-for="product in products" :key="product.name">
          <div>{{ product.name }}</div>
          <div>{{ product.qty }}</div>
          <div>${{product.qty * product.price}}.00</div>
          <button @click="addTo(product)">Add</button>
          <button @click="removeFrom(product)">Remove</button>
        </div>
        <div class="cart-total">
          <div>Grand Total</div>
          <div class="total">${{Total}}.00</div>
        </div>
      </div>
  </div>
</template>

<script>

export default {
  name: "HelloWorld",
  data() {
    return {
      products: [
        { id: 0, name: "star wars", price: 50, qty: 5 },
        { id: 1, name: "nfl", price: 20, qty: 6 },
        { id: 2, name: "nhl", price: 30, qty: 2 }
      ]
    };
  },
  computed: {
    Total: function() {
      var total = 0;
      this.products.forEach(product => {
        total += (product.price * product.qty);
      });
      return total;
    }
  },
  methods: {
    addTo(product) {
      product.qty++;
    },
    removeFrom(product) {
      product.qty--;
      if (product.qty < 1 ) {
        const thisIndex = this.products.indexOf(product);
        this.products.splice(thisIndex, 1);
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .cart {
    display: grid;
  }
  .cart-header {
    display: grid;
    grid-template-columns: repeat(5, 1fr);
  }
  .cart-product {
    display: grid;
    grid-template-columns: repeat(5, 1fr);
  }
  .cart-total {
    display: grid;
    grid-template-columns: repeat(5, 1fr);
  }
  .total {
    grid-column: 3;
  }
  button {
    width: 60px;
  }

</style>
