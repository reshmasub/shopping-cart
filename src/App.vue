<template>
  <div>
    <div class="container">
      <div class="row">
        <div class="col-md-7">
          <div class="row">
            <div class="col-md-6" v-for="product in products" :key="product.id">
              <product :isInCart = "isInCart(product)" v-on:add-to-cart="addToCart($event)" :product="product"></product>
            </div>
          </div>
        </div>
        <div class="col-md-5 my-5">
          <cart v-on:pay="pay()" v-on:remove-from-cart="removeFromCart($event)"  :items="cart">

          </cart>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import products from "@/products.json";
import Product from "@/components/Product.vue";
import Cart from "@/components/Cart.vue"
export default {
  name: "app",
  components: {
    Product, 
    Cart
  },
  data() {
    return {
      products,
      cart: []
    };
  },
  methods: {
    addToCart(product) {
      this.cart.push(product);
    },
    isInCart(product){
      const item = this.cart.find(item => item.id=== product.id);
      if(item)
      return true;
      else
      return false;
    },
    removeFromCart(product){
      this.cart = this.cart.filter(item => item.id != product.id)
    },
    pay(){
      this.cart = []
      alert('Shoping Completed')
    }
  }
};
</script>

<style>
body {
  background-color: #f8f8f3;
}
</style>
