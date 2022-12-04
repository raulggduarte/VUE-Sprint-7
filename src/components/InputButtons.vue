<template>
  <div class="btn-container">
    <button
      type="button"
      class="btn-square btn-orange"
      @click="$emit('update-qty', option.qty++)"
    >
      +
    </button>
    <input
      class="input"
      type="number"
      min="0"
      v-model="option.qty"
      @input="$emit('update-qty')"
    />
    <button
      type="button"
      class="btn-square btn-orange"
      @click="$emit('update-qty', option.qty === 0 ? option.qty : option.qty--)"
    >
      -
    </button>
  </div>
</template>

<script>
export default {
  name: "InputButtons",
  props: {
    option: Object,
  },
};
</script>

<style scoped>
.btn-container {
  display: flex;
  align-items: center;
  margin: 0;
}
.btn-square {
  width: 35px;
  height: 35px;
  line-height: 35px;
  font-family: arial;
  font-size: xx-large;
  border: none;
  border-radius: 5px;
}
.btn-orange {
  background-color: orange;
  color: white;
}
input {
  width: 70px;
  height: 35px;
  font-size: large;
  border: none;
  padding: 5px;
  text-align: center;
}
input:focus {
  border: 2px solid black;
  border-radius: 5px;
  outline: none;
}
/* Chrome, Safari, Edge, Opera */
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

/* Firefox */
input[type="number"] {
  -moz-appearance: textfield;
}
</style>