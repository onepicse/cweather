<template>
	<i class="iconfont" :class="className" :style="{color: color, fontSize: size + 'px'}"></i>
</template>

<script>
export default {
  name: 'Icon',
  data () {
    return {
    }
  },
  props: {
    iconClass: {
      type: String,
      required: true
    },
    size: {
      type: Number,
      default: 44
    },
    color: {
      type: String,
      default: '#fff'
    }
  },
  computed: {
    className () {
      return 'icon-' + this.iconClass
    }
  }
}
</script>

<style lang="less">
.iconfont{
  display: inline-block;
  vertical-align: middle;
  width: 0.586667rem;
  height: 0.586667rem;
  line-height: 1;
}
</style>
