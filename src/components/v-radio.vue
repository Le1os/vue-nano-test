<template>
  <div class="my-radio">
    <label>
    <input type="radio"
           :value="value"
           @change="$emit('update:modelValue', $event.target.value)"
           :checked="value === modelValue"
    >
    
    <slot/>
  </label>
</div>
</template>

<script>
  export default {
    name: "v-radio",
    props: {
      value: { type: String, default: null, },
      modelValue: { type: String, default: null, },
    }
  }
</script>

<style scoped>
  .my-radio {
    background: #ffffff;
    padding: 6px 12px;
    margin: 8px 0;
    display: inline-block;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
    min-height: 33px;
    min-width: 222px;
    position: relative;
    display: flex;
    flex-wrap: wrap;
  }
</style>