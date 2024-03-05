<template>
  <div id="total-value">Balance: {{ total }}</div>
</template>

<script>
export default {
  name: "TotalBalance",
  props: {
    total: {
      type: Number,
      default: 0,
    },
  },
};
</script>

<style scoped>
#total-value {
  font-size: 1.3rem;
  text-transform: uppercase;
  padding: 0.5rem;
  text-align: center;
  display: block;
}
</style>
