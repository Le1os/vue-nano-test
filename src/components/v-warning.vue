<template>
  <div class="my-warning" fieldName="fieldName">Please fill {{fieldName}} field!</div>
</template>

<script>
export default {
  name: 'v-warning',
  props: {
    fieldName: [String]
  }
}
</script>

<style scoped>
.my-warning {
  display: flex;
  /* justify-content: center; */
  /* margin: 2% 40% 0% 40%; */
  /* border: 1px solid teal; */
  /* padding: 4px 2px; */

  color: red;
  /* padding: 40px 20px; */
  margin-left: 1%;
  /* display: inline-block;
  /* border: 1px solid #ccc;
  border-radius: 2px;
  box-sizing: border-box;
  min-height: 32px;
  min-width: 220px;
  position: relative;
  display: flex;
  flex-wrap: wrap; */
}

</style>