<template>
  <div class="total-value-green" v-if="total>0">
    Balance: {{ total }}
  </div>
  <div class="total-value-black" v-else-if="total==0">
    Balance: {{ total }}
  </div>
  <div class="total-value-red" v-else-if="total<0">
    Balance: {{ total }}
  </div>
</template>

<script>
export default {
  name: 'TotalBalance',
  props: {
    total: {
      type: Number,
      default: 0,
    }
  }
}
</script>

<style scoped>
  .total-value-green {
    font-size: 26px;
    text-transform: uppercase;
    padding: 20px;
    text-align: center;
    color: green;
  }
  .total-value-black {
    font-size: 26px;
    text-transform: uppercase;
    padding: 20px;
    text-align: center;
    color: black;
  }
  .total-value-red {
    font-size: 26px;
    text-transform: uppercase;
    padding: 20px;
    text-align: center;
    color: red;
  }
</style>