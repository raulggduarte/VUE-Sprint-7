<template>
  <div :class="product.name" class="container">
    <div v-for="option in product.options" :key="option.id">
        <p>{{ option.text }}</p>
        <InputButtons
          :option="option"
          @update-qty="
            $emit('update-options', option.qty, product.id, option.id)
          "
        />
        <Modal :text="option.modalText" :id="option.id" :tag="option.tag"/>
    </div>
  </div>
</template>

<script>
import InputButtons from "./InputButtons";
import Modal from "./Modal"

export default {
  name: "Panel",
  components: {
    InputButtons,
    Modal,
  },
  props: {
    product: Object,
  },
};
</script>

<style scoped>
.container {
  flex-direction: column;
  width: 460px;
  border: 3px solid black;
  border-radius: 10px;
  margin: 10px;
  padding: 30px 20px 10px 20px;
}
div {
  margin-bottom: 20px;
  display: flex;
}
p {
  margin: auto 5px;
  padding-right: 5px;
  width: 150px;
}
</style>