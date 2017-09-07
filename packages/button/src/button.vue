<template>
  <button :disabled="disabled" class="btn"
    @click="handleClick"
    :autofocus="autofocus"
    :type="nativeType"
    :class="[
      type ? 'btn-' + type : '',
      size ? 'el-button--' + size : '',
      loading ? 'spinner spinner-default spinner-sm' : '',
      {
        'is-disabled': disabled,
        'is-plain': plain
      }
    ]"
  >
    <i :class="'el-icon-' + icon" v-if="icon && !loading" @click="handleInnerClick"></i>
    <span v-if="$slots.default" @click="handleInnerClick"><slot></slot></span>
  </button>
</template>
<script>
  export default {
    name: 'ElButton',

    props: {
      type: {
        type: String,
        default: 'default'
      },
      size: String,
      icon: {
        type: String,
        default: ''
      },
      nativeType: {
        type: String,
        default: 'button'
      },
      loading: Boolean,
      disabled: Boolean,
      plain: Boolean,
      autofocus: Boolean
    },

    methods: {
      handleClick(evt) {
        this.$emit('click', evt);
      },
      handleInnerClick(evt) {
        if (this.disabled) {
          evt.stopPropagation();
        }
      }
    }
  };
</script>
