<template>
  <div id="app">
    <!-- <img src="./assets/greensock.png" alt=""> -->
        <div class="cart">
            <p>Cart({{cart.length}})</p>
        </div>
        <product :premium="premium" @add-to-cart="updateCart"></product>
  </div>
</template>

<script>
import product from './components/product.vue'

export default {
  name: 'App',
  data(){
    return{
    premium: false,
    cart: [],}
  },
  methods: {
    updateCart(id) {
      this.cart.push(id);
    },
  },
  components: {
    product
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

    .color-box{
        width: 40px;
        height: 40px;
        margin-top: 5px;
        margin: auto;
    }
    .disabledButton{
        color: red;
    }
</style>
