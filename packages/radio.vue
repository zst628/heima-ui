 <template>
  <div>
    <label class="cs-radio" :class="{'is-checked' : label === modal}">
      <span class="cs-radio__input">
        <span class="cs-radio__inner"></span>
        <input v-model="modal" :name="name" :value="label" type="radio" class="cs-radio__original" />
      </span>
      <div class="cs-radio__label">
          <slot></slot>
          <!-- 如果没有传内容  就把 label 当成内容 -->
          <template v-if="!$slots.default">
              {{label}}
          </template>
      </div>
    </label>
  </div>
</template>

<script>
export default {
  name: "HmRadio",
  inject:{
    RadioGroup:{
      default:''
    }
  },
    
//  需要提供一个计算属性 modal
computed: {
    modal: {
        get() {
            return this.isGroup ? this.RadioGroup.value : this.value
        },
        set(value) {
            // 触发父组件给当前组件注册的input事件
            this.$emit('input', value);
            this.isGroup ? this.RadioGroup.$emit('input',value) : this.$emit('input',value)
        }
    },
    isGroup () {
      // 用于判断radio是否被RadioGroup所包裹
      return !!this.RadioGroup
    }
},
  props: {
    label: {
      type: [String, Number, Boolean],
      defualt: "",
    },
    value: null,
    name: {
      type: String,
      defualt: "",
    },
  },
};
</script>

<style lang="scss" scoped>
.cs-radio {
  color: #606266;
  font-weight: 500;
  line-height: 1;
  position: relative;
  cursor: pointer;
  display: inline-block;
  white-space: nowrap;
  outline: none;
  font-size: 14px;
  margin-right: 30px;
  -moz-user-select: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  &__input {
    white-space: nowrap;
    cursor: pointer;
    outline: none;
    display: inline-block;
    line-height: 1;
    position: relative;
    vertical-align: middle;
    .cs-radio__inner {
      border: 1px solid #dcdfe6;
      border-radius: 100%;
      width: 14px;
      height: 14px;
      background-color: #fff;
      position: relative;
      cursor: pointer;
      display: inline-block;
      box-sizing: border-box;
      &:after {
        width: 4px;
        height: 4px;
        border-radius: 100%;
        background-color: #fff;
        content: "";
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%) scale(0);
        transition: transform 0.15s ease-in;
      }
    }
    .cs-radio__original {
      opacity: 0;
      outline: none;
      position: absolute;
      z-index: -1;
      top: 0;
      left: 0px;
      right: 0;
      bottom: 0;
      margin: 0;
    }
  }
  .cs-radio__label {
    font-size: 14px;
    padding-left: 10px;
  }
}
// 选中的样式
.cs-radio.is-checked {
  .cs-radio__input {
    .cs-radio__inner {
      border-color: #409eff;
      background-color: #409eff;
      &:after {
        transform: translate(-50%, -50%) scale(1);
      }
    }
  }
  .cs-radio__label {
    color: #409eff;
  }
}
</style>
