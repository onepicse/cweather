<template>
  <div id="app" class="cold">
    <div class="bottom-nav">
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {

    }
  },
  computed: {

  },
  watch: {

  },
  beforeCreat () {

  },
  created () {

  },
  beforeMount () {

  },
  Mounted () {

  },
  beforeDestroy () {

  },
  destroyed () {

  }
}
</script>

<style lang="less">
html,body {
  position: relative;
  width: 100%;
  height: 100%;
}
body{
  -webkit-tap-highlight-color:rgba(0, 0, 0, 0);line-height:12px;-webkit-user-select:none;word-break:break-all;word-wrap:break-word;font-family: Helvetica, Tahoma, Arial, "PingFang SC", "Hiragino Sans GB", "Heiti SC", "Source Han Sans SC", "Microsoft YaHei", "WenQuanYi Micro Hei", sans-serif;
}
#app{
  width: 100%;
  height: 100%;
  position: relative;
  .bottom-nav{
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 1.76rem;
  }
  &.sunny{
    background-image: linear-gradient( 0deg, #FCCF31 10%, #F55555 100%);
    .bottom-nav{
      background-color: #F55555;
    }
  }
  &.cold{
    background-image: linear-gradient( 0deg, #ABDCFF 10%, #0396FF 100%);
    .bottom-nav{
      background-color: #0396FF;
    }
  }
}

</style>
