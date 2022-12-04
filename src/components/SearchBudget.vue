<template>
  <div class="container">
    <input
      type="text"
      v-model="text"
      placeholder="Busca un pressupost"
      @input="$emit('budget-name', this.text.trim())"
      class="inputForm"
    />
  </div>
</template>

<script>
export default {
  name: "SearchBudget",
  data() {
    return {
      text: "",
    };
  },
};
</script>

<style scoped>
.container {
    display: flex;
    flex-direction: column;
}
.inputForm{
    margin-bottom: 20px;
    width: 90%;
}
</style>