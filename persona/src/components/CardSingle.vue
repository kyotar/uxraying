<template>
  <div class="card">
    <input type="text" :placeholder="placeholder" :maxlength="maxlength">
  </div>
</template>

<script>
export default {
  name: 'card',
  props: {
    placeholder: String,
    maxlength: Number
  }
}
</script>

<style lang="scss" scoped>

</style>
