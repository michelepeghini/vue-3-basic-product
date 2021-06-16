<template>
  <div class="nav-bar">
    <h1>{{ title }}</h1>
  </div>
</template>

<script>
export default {
  name: 'NavBar',
  props: {
    title: {
      type: String,
      default: 'Title'
    }
  }
}
</script>

<style lang="scss" scoped>
.nav-bar {
  background: linear-gradient(-90deg, #84cf6a, #16c0b0);
  height: 70px;
  margin-bottom: 25px;
  -webkit-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  box-shadow: 1px 1px 5px rgba(0, 0, 0, 0.57);

  h1 {
    padding-left: 20px;
    margin-block-start: 0;
    margin-block-end: 0;
  }
}
</style>
