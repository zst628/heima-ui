<template>
  <div class="cs-radio-group">
      <slot></slot>
  </div>
</template>

<script>
export default {
  name:'HmRadioGroup',
  provide() {
      return {
          RadioGroup:this,
      }
  },
  props: {
    //   hm-radio-group 接收到了 value值
    //   将来还需要触发  当前的input事件
    //  vue: provide 与 inject  react:provider/consumer
      value:null
  },
  data() {
    return {};
  },
};
</script>

<style>
</style>
