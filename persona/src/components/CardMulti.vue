<template>
  <div class="card">
    <textarea :placeholder="placeholder" :rows="rows"></textarea>
  </div>
</template>

<script>
// import Init from './CommonScript.vue';

export default {
  name: 'card',
  props: {
    placeholder: String,
    rows: String
  }
}
</script>

<style lang="scss" scoped>
.card {
  textarea {
    resize: none;
  }
}
</style>
