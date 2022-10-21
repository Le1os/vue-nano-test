<template>
  <label class="my-multiselect">
    <input type="checkbox"
           :value=value
           @click="e => onChange(e)"
           >

    <slot></slot>
  </label>
</template>
  
<script>
  export default {
    name: "v-checkbox",
    props: {
      value: { type: [String], default: null, },
      modelValue: { type: [Array, Boolean], default: null },
    },
    methods: {
      onChange(v) {
        let val = v.target.value
        
        console.log(val, this.value , this.modelValue, this.$);
        if (typeof this.modelValue == 'boolean')  
        this.$emit("update:modelValue", !this.modelValue);
        
        else if (!this.modelValue.includes(val)) {
          this.$emit('update:modelValue', [...this.modelValue, val]);
        } 
        else {
            this.$emit('update:modelValue', this.modelValue.filter(v => v !== val));
        }
      }
      
    },
  }
</script>



<style scoped>
    .my-multiselect{
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