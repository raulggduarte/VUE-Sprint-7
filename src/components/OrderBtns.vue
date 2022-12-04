<template>
  <div class="btn-container">
    <button
      class="btn btn-outline-dark"
      type="button"
      @click="$emit('order-budgets', 'alfa')"
    >
      Ordre alfabètic
    </button>
    <button
      class="btn btn-outline-dark"
      type="button"
      @click="$emit('order-budgets', 'date')"
    >
      Ordre per data
    </button>
    <button
      class="btn btn-outline-dark"
      type="button"
      @click="$emit('order-budgets', 'reset')"
    >
      Reiniciar ordre
    </button>
  </div>
</template>

<script>
export default {
  name: "OrderBtns",
};
</script>

<style scoped>
.btn {
  margin: 0 10px 20px 10px;
}
.btn:hover {
  color: black !important;
  background-color: rgb(217, 154, 36) !important;
  border-color: rgb(217, 154, 36) !important;
}
</style>