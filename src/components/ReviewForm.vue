<template>
  <form class="review-form" @submit.prevent="onSubmit">
    <h3>Leave a review</h3>
    <label for="name">Name:</label>
    <input id="name" v-model="name" />

    <label for="review">Review:</label>
    <textarea id="review" v-model="text"></textarea>
    <label for="rating">Rating:</label>
    <select id="rating" v-model.number="rating">
      <option>5</option>
      <option>4</option>
      <option>3</option>
      <option>2</option>
      <option>1</option>
    </select>

    <input class="button" type="submit" value="Submit" />
  </form>
</template>

<script>
export default {
  name: 'ReviewForm',
  data () {
    return {
      name: '',
      text: '',
      rating: null
    }
  },
  methods: {
    onSubmit () {
      if (this.name === '' || this.text === '' || this.rating === null) {
        alert('Please fill out every field.')
        return
      }

      const review = {
        name: this.name,
        text: this.text,
        rating: this.rating
      }
      this.$emit('review-submitted', review)
      this.name = ''
      this.text = ''
      this.rating = null
    }
  },
  emits: ['review-submitted']
}
</script>

<style lang="scss" scoped>
.review-form {
  display: flex;
  flex-direction: column;
  width: 425px;
  padding: 20px;
  margin: 40px;
  border: 2px solid #d8d8d8;
  background-color: white;
  -webkit-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  box-shadow: 2px 15px -12px rgba(0, 0, 0, 0.57);

  .button {
    display: block;
    margin: 30px auto;
  }
}
</style>
