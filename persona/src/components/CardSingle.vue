<template>
  <div class="card">
    <input type="text" :placeholder="placeholder" :maxlength="maxlength" @change="setStorage">
  </div>
</template>

<script>
// import CommonScript from './CommonScript.vue';

export default {
  name: 'card',
  // mixins: [CommonScript],
  props: {
    placeholder: String,
    maxlength: String
  }
}
</script>

<style lang="scss" scoped>

</style>
