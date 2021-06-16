<template>
  <div class="cart">
    <p>Cart ({{ itemsCount }})</p>
    <ul>
      <li v-for="(cartItem, index) in cartItems" :key="index">
        {{
          `${cartItem.item.name} - ${cartItem.item.color} X ${cartItem.quantity}`
        }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Cart',
  props: {
    cartItems: {
      type: Array,
      default () {
        return []
      }
    }
  },
  computed: {
    itemsCount () {
      return this.cartItems.reduce(function (acc, curr) { return acc + curr.quantity }, 0)
    }
  }
}
</script>

<style lang="scss" scoped>
.cart {
  margin: 25px 100px;
  float: right;
  border: 1px solid #d8d8d8;
  padding: 10px 30px;
  background-color: white;
  -webkit-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  box-shadow: 2px 15px -12px rgba(0, 0, 0, 0.57);
}
</style>
