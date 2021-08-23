<template>
 <div class="product">
    <div class="product-image">
    <img v-bind:src="image" alt="">
    </div>
    <div class="product-info">
        <h1>{{ title }}</h1>
        <p v-if="inStock">In stock</p>
        <p v-else>Out of stock</p>
        <p>Shipping:{{ shipping }}</p>
        <ul>
            <li v-for="detail in details" :key="detail">{{ detail }}</li>
        </ul>
        <div v-for="(variant,index) in variants" :key="variant.variantId" class="color-box" :style="{ backgroundColor:variant.variantColor }" @mouseover="updateProduct(index)">
        </div>
        <button v-on:click="addToCart" :disabled="!inStock" :class="{ disabledButton:!inStock }">Add to Cart</button>
    </div>
    <div>
    <h2>Reviews</h2>
    <p v-if="!reviews.length">There are no reviews yet.</p>
    <ul>
    <li v-for="review in reviews" :key="review">
    <p>{{ review.name }}</p>
    <p>Rating: {{ review.rating }}</p>
    <p>{{ review.review }}</p>
    </li>
    </ul>
    </div>
    <product-review @review-submitted="addReview"></product-review>
</div>
</template>

<script>
import productReview from './productReview.vue'

export default {
  name: 'product',
    components: {
    productReview
  },
  data() {
    return {
      brand: "vue",
      product: "Socks",
      selectedVarient: 0,
      details: ["80%cotton", "20%polyester", "gender-neutral"],
      variants: [
        {
          variantId: 2234,
          variantColor: "green",
          variantImage: require("../assets/greensock.png"),
          variantQuantity: 10,
        },
        {
          variantId: 2235,
          variantColor: "blue",
          variantImage: require("../assets/bluesock.png"),
          variantQuantity: 0,
        },
      ],
      reviews: [],
    };
  },
  methods: {
    addToCart() {
      this.$emit("add-to-cart", this.variants[this.selectedVarient].variantId);
    },
    updateProduct(index) {
      this.selectedVarient = index;
      console.log(index);
    },
    addReview(productReview) {
      this.reviews.push(productReview);
    },
  },
  computed: {
    title() {
      return this.brand + "" + this.product;
    },
    image() {
      return this.variants[this.selectedVarient].variantImage;
    },
    inStock() {
      return this.variants[this.selectedVarient].variantQuantity;
    },
    shipping() {
      if (this.premium) {
        return "Free";
      }
      return "2.99";
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
