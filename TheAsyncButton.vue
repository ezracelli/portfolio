<template>
  <button
    @click="doAction()"
    :class="{ disabled: waitingForResponse }"
    class="async-button btn"
  >
    <div class="img-container">
      <img
        v-if="waitingForResponse"
        src="@/assets/img/loading.gif"
        alt="Loading..."
      >
    </div>
    <span
      :class="{ invisible: waitingForResponse }"
      class="d-flex align-items-center justify-content-center"
    >
      <slot></slot>
    </span>
  </button>
</template>

<script>
export default {
  props: {
    action: {
      type: Function,
      required: true,
    },
    args: {
      type: Array,
      default: () => [],
    },
  },
  data () {
    return { waitingForResponse: false }
  },
  methods: {
    doAction () {
      this.waitingForResponse = true
      
      this.action(...this.args)
        .then(res => this.$emit('then', res))
        .catch(res => this.$emit('catch', res))
        .finally(() => {
          this.waitingForResponse = false
        })
    },
  },
}
</script>

<style scoped lang="scss">
.img-container {
  top: 0.25rem;
  bottom: 0.25rem;
  left: 0.25rem;
  right: 0.25rem;
  position: absolute;

  img {
    height: 100%;
  }
}
</style>
