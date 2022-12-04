<template>
  <i
    class="fas fa-circle-info"
    data-bs-toggle="modal"
    :data-bs-target="`#inputModal_${tag}_${id}`"
  ></i>
  <div
    class="modal fade"
    :id="`inputModal_${tag}_${id}`"
    tabindex="-1"
    :aria-labelledby="`inputModalLabel_${tag}`"
    aria-hidden="true"
  >
    <div class="modal-dialog modal-lg modal-dialog-centered">
      <div class="modal-content border border-dark border-3 rounded-4">
        <div class="modal-body text-center">
          {{ text }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Modal",
  props: {
    text: String,
    id: Number,
    tag: String,
  },
};
</script>

<style scoped>
.fas {
  color: rgb(182, 182, 182);
  font-size: 25px;
  padding: 5px;
}
.fas:hover {
  cursor: pointer;
}
</style>