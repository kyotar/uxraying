<template>
  <div class="card">
    <textarea :placeholder="placeholder" :rows="rows"></textarea>
  </div>
</template>

<script>
export default {
  name: 'card',
  props: {
    placeholder: String,
    rows: Number
  }
}
</script>

<style lang="scss" scoped>
.card {
  textarea {
    resize: none;
    // height: 400px;
  }
}
</style>
