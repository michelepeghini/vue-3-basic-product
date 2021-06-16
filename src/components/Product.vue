<template>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <a :href="url" target="_blank">
          <img
            :src="selectedVariant.image"
            :alt="`Image for ${name}`"
            :title="name"
          />
        </a>
      </div>
      <div class="product-description">
        <h2>{{ name }}</h2>
        <p v-if="onSale">On Sale</p>
        <p :class="stockLevelColor">{{ inStockMessage }}</p>
        <p>Variants:</p>
        <select v-model="selectedVariant" name="variant">
          <option
            v-for="variant in variants"
            :key="variant.id"
            :value="variant"
          >
            {{ variant.color }}
          </option>
        </select>
        <p>Materials:</p>
        <ul>
          <li v-for="item in description" :key="item.id">{{ item }}</li>
        </ul>
        <button
          class="button"
          @click="addToCart"
          :disabled="!selectedVariant.stock"
          :class="{ disabledButton: !selectedVariant.stock }"
        >
          Add to Cart
        </button>
      </div>
    </div>
    <ReviewList :reviews="reviews" />
    <ReviewForm @review-submitted="addReview" />
  </div>
</template>

<script>
import ReviewForm from './ReviewForm.vue'
import ReviewList from './ReviewList.vue'

export default {
  name: 'Product',
  components: {
    ReviewForm,
    ReviewList
  },
  data () {
    return {
      name: 'My Product',
      description: ['50% cotton', '30% wool', '20% polyester'],
      url: 'https://www.vuemastery.com',
      onSale: true,
      variants: [
        { id: 1000, color: 'green', image: require('@/assets/images/socks_green.jpg'), stock: 50 },
        { id: 1001, color: 'blue', image: require('@/assets/images/socks_blue.jpg'), stock: 10 }
      ],
      selectedVariant: {},
      reviews: [],
      tabs: ['ReviewForm', 'ReviewList'],
      activeTab: 'ReviewForm'
    }
  },
  computed: {
    inStockMessage () {
      let msg = 'In Stock'
      if ((this.selectedVariant.stock < 10) && (this.selectedVariant.stock > 0)) {
        msg = 'Almost finished'
      } else if (this.selectedVariant.stock <= 0) {
        msg = 'Out of stock!'
      }
      return msg
    },
    stockLevelColor () {
      let color = 'green'
      if ((this.selectedVariant.stock < 10) && (this.selectedVariant.stock > 0)) {
        color = 'orange-red'
      } else if (this.selectedVariant.stock <= 0) {
        color = 'red'
      }
      return color
    }
  },
  methods: {
    addToCart () {
      const payload = this.selectedVariant
      payload.name = this.name
      this.$emit('add-to-cart', payload)
    },
    addReview (review) {
      this.reviews.push(review)
    }
  },
  emits: ['add-to-cart'],
  mounted () {
    this.selectedVariant = this.variants[0]
  }
}
</script>

<style lang="scss" scoped>
.product-display {
  display: flex;
  flex-direction: column;
  padding: 1rem;
}

.product-container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}

.product-image,
.product-info {
  width: 50%;
}
</style>
