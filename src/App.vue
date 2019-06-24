<template>
  <div id="app">
    <first @show="show"></first>
    <div class="App animated bounceInLeft" v-show="visible">
      <div class="date"></div>
      <div id="autotype">
        <h3 style="font-weight:900">给...</h3>
        <p>😏</p>

        <div style="text-align:right">
          <p>xx</p>
          <p>2019年6月22日</p>
        </div>
      </div>
      <audio ref="audio" :src="bgm"></audio>
    </div>
  </div>
</template>

<script>
import bgm from './assets/bgm.mp3'
import $ from 'jquery'
import First from './components/First'
export default {
  name: 'app',
  components: {
    First
  },
  data() {
    return {
      visible: false
    }
  },
  computed: {
    bgm: function () {
      return bgm;
    }
  },
  methods: {
    show: function () {
      this.visible = true
      this.print()
      this.$refs.audio.play()
    },
    print: function () {
      $.fn.autotype = function() {
        var _this=$(this);
        var str=_this.html();
        // 正则替换代码行之间添加的多个空格，不去除换行输出会有明显的停顿：实际是在输出多个空格
        str=str.replace(/(\s){2,}/g,"$1");
        var index = 0;
        $(this).html('');
        var timer = function fn() {
          var args=arguments;
          var current = str.slice(index, index+1);
          // html标签完整输出,如：<p>
          if (current == '<'){
            index = str.indexOf('>', index) + 1;
          }
          else{
            index++;
          }
          //位运算符: 根据setInterval运行奇偶次来判断是否加入下划线字符“_”，使输入效果更逼真
          if (index < str.length-1){ //打印字符倒数第2个字符开始，不加下划线字符，以防止结束符可能会多输出一下划线字符
            _this.html(str.substring(0, index) + (index & 1 ? '_' : ''));
          }else{
            _this.html(str.substring(0, index));
            clearTimeout(timer);
          };
          setTimeout(fn,100)
        };
        // 延迟1s开始
        setTimeout(timer,1000);
      };
      $("#autotype").autotype();
    }
  }
}
</script>

<style>
@import "assets/css/App.css";
@import 'assets/css/index.css';
  p {
    line-height: 25px
  }
</style>
