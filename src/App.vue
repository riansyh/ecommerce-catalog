<template>
  <ProductDisplay />
</template>

<script>
import ProductDisplay from './components/ProductDisplay.vue'

export default {
  name: 'App',
  components: {
    ProductDisplay
  }
}
</script>

<style>
:root {
  --blue: #002772;
  --pink: #FDE2FF;
  --brown: #1E1E1E;
  --purple: #720060;
  --ligh-blue: #D6E6FF;
  --gray: #3F3F3F;
  --light-gray: #DCDCDC;
  --white: #FFFFFF;
}

#app {
  font-family: Inter, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
