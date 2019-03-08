<template>
<textarea
  v-bind="{ value, rows }"
  @input="$emit('input', $event.target.value)"
  class="autosize-textarea form-control"
/>
</template>

<script>
// adapted from https://github.com/egoist/vue-autosize-textarea/issues/1#issuecomment-356509633

import autosize from 'autosize'

export default {
  props: {
    value: String,
    rows: {
      type: Number,
      default: 2,
    },
  },
  mounted () {
    autosize(this.$el)
  },
}
</script>

<style scoped>
.autosize-textarea {
  padding: 7px;
  width: 100%;
}
</style>
