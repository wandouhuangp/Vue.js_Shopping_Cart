<template>
  <span>
    <button v-on:click="$emit('changeQuantity', id, 1)">+</button>
    <button v-on:click="$emit('changeQuantity', id, -1)">-</button>
  </span>
</template>

<script>
export default {
  props: ["id"]
};
</script>

<style scoped>
</style>


