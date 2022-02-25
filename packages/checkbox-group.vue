<template>
  <div class="cs-checkbox-group">
    <slot></slot>
  </div>
</template>
<script>
export default {
  name: 'HmCheckboxGroup',
  provide () {
    return {
      checkboxGroup: this
    }
  },
  props: {
    value: {
      // get an array
      type: Array
    }
  }
}
</script>
