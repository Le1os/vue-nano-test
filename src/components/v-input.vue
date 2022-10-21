<template>
    <input class="input" type="text"
           :inputType="inputType" :value="modelValue" @input="updateInput">
</template>
  
  <script>
  export default {
    name: 'my-input',
    props: {
      modelValue: [String, Number],
      inputType: String
    },
    methods: {
      updateInput(event) {
        this.$emit('update:modelValue', event.target.value)
      }
    }
  }
  </script>
  
  <style scoped>
  .input {
    display: flex;
    flex-wrap: wrap;
    background: #ffffff;
    padding: 4px 12px;
    margin: 6px 0;
    border: 1px solid #ccc;
    border-radius: 2px;
    box-sizing: border-box;
    min-height: 32px;
    min-width: 220px;
    position: relative;
  }
  
  </style>