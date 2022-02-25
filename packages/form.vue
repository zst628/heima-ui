<template>
  <div class="cs-form">
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: "HmForm",
  provide () {
    return {
      Form: this
    }
  },
  props: {
    model: {
      type: Object,
      required: true
    },
    labelWidth: {
      type: String,
      default: '120px'
    }
  }
};
</script>

<style>
</style>
