<template>
  <div id="app">
    <OrderForm>

    </OrderForm>

  </div>
</template>

<script>
import OrderForm from './components/OrderForm.vue'
// import Preview from './components/Preview.vue'
export default {
  name: 'App',
  components: {
    OrderForm,
    // Preview
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
  margin: 0;
  padding: 0;
  outline: none;
  overflow: auto;
}
</style>
