<template>
  <div id="app" class="cold">
    <transition name="fadeInDown">
      <div v-if="ready" class="weather-icon iconfont" :class="weatherCode">
      </div>
    </transition>
    <p v-if="ready" class="weather-text">{{now.text}}</p>
    <p class="location">{{location}}</p>
    <div class="info">
      {{now.temperature}}
    </div>
    <div class="bottom-nav">
      <Icon class="pull-left" :iconClass='"question-mark"' :color='"#fff"'></Icon>
      <Icon class="pull-right" :iconClass='"add"' :color='"#fff"'></Icon>
    </div>
  </div>
</template>

<script>
import Icon from './components/Icon.vue'
const UID = 'U9CD56396F'
const KEY = 'l9clhm4p2oygrhan'
const API = 'http://api.seniverse.com/v3/weather/now.json' // 获取天气实况接口
export default {
  name: 'App',
  data () {
    return {
      ready: false,
      location: '北京',
      now: {
        code: '0',
        temperature: '0',
        text: '晴'
      }
    }
  },
  computed: {
    weatherCode () {
      return 'icon-code_' + this.now.code
    }
  },
  watch: {

  },
  beforeCreat () {

  },
  created () {
    // 读取localstorge中的数据
  },
  beforeMount () {

  },
  mounted () {
    // 进行调取数据
    let ts = Math.floor((new Date()).getTime() / 1000)
    // 构造验证参数字符串
    let str = 'ts=' + ts + '&uid=' + UID
    // 使用 HMAC-SHA1 方式，以 API 密钥（key）对上一步生成的参数字符串（raw）进行加密
    // 并将加密结果用 base64 编码，并做一个 urlencode，得到签名 sig
    let sig = window.CryptoJS.HmacSHA1(str, KEY).toString(window.CryptoJS.enc.Base64)
    sig = encodeURIComponent(sig)
    str = str + '&sig=' + sig
    // 构造最终请求的 url
    let url = API + '?location=' + this.location + '&' + str

    this.$http.jsonp(url).then((res) => {
      let data = res.body.results[0]
      console.log(data)
      this.ready = true
      this.now = data.now
    })
  },
  beforeDestroy () {
    // 把数据保存到localstorge
  },
  destroyed () {

  },
  components: {
    Icon: Icon
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
  .weather-icon{
    width: 100%;
    height: 4.8rem;
    padding-top: 2.666667rem;
    padding-bottom: 1.0rem;
    font-size: 4.8rem;
    line-height: 1;
    color: #fff;
    text-align: center;
  }
  .weather-text {
    font-size: 90px;
    line-height: 1;
    color: #fff;
    text-align: center;
  }
  .location {
    margin: 0.8rem 0;
    font-size: 36px;
    color: #fff;
    line-height: 1;
    text-align: center;
  }
  .info {
    width: 100%;
    height: 2.133333rem;
    background-color: rgba(255, 255, 255, .43)
  }
  .bottom-nav{
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 1.76rem;
    padding: 0.586667rem 0.4rem;
    text-align: justify;
    box-sizing: border-box;
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
.pull-left {
  float: left;
}
.pull-right {
  float: right;
}
.fadeInDown-enter-active {
  animation: fadeInDown 1s;
}
.fadeInDown-leave-active {
  animation: fadeInDown 1s reverse;
}
@keyframes fadeInDown{
  0% {
    opacity: 0;
    transform: translate3d(0, -50%, 0);
  }
  100% {
    opacity: 1;
    transform: translate3d(0, 0, 0);
  }
}
</style>
