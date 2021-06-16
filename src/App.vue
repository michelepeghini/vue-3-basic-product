<template>
  <NavBar :title="title" />

  <Cart :cartItems="cart" />

  <Product @add-to-cart="addToCart" />
</template>

<script>
import NavBar from './components/NavBar.vue'
import Cart from './components/Cart.vue'
import Product from './components/Product.vue'

export default {
  name: 'App',
  data () {
    return {
      title: 'My Title',
      cart: []
    }
  },
  components: {
    NavBar,
    Cart,
    Product
  },
  methods: {
    addToCart (item) {
      const itemPos = this.cart.findIndex(function (cartItem) { return cartItem.item.id === item.id })
      if (itemPos !== -1) {
        this.cart[itemPos].quantity += 1
      } else {
        const newItem = {
          quantity: 1,
          item: item
        }
        this.cart.push(newItem)
      }
    }
  }
}
</script>

<style>
@import "styles.css";
</style>
