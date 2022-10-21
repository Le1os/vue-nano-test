<template>
  <button class="my-button"
    >
    Вiдправити
  </button>
</template>

<script>
export default {
  name: 'v-button',
  props: {
    modelValue: [String]
  },
  // methods: {
  //   updateInput(event) {
  //     this.$emit('update:modelValue', event.target.value)
  //   }
  // }
}
</script>

<style scoped>
.my-button {
  display: flex;
  justify-content: center;
  margin: 2% 40% 0% 40%;
  background-color: orange;
  border: 1px solid teal;
  border-radius: 4px;
}

</style>