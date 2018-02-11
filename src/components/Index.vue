<template>
<div class="container">
  <elSearch></elSearch>
  <elNav></elNav>
  <h2 class="l-tit">推荐内容</h2>
  <elList></elList>
</div>
</template>
<script>
import elSearch from '@/components/Search.vue'
import elNav from '@/components/Nav.vue'
import elList from '@/components/List.vue'
export default {
  name: 'news-list',
  components: {
    elSearch : elSearch,
    elNav : elNav,
    elList : elList
  },
  data () {
    return {
      list: null,
      apiURL: 'http://zy.cnhubei.com/m/dongxiang/news/list?psize=20&rechid=999999999999999999&infoid=null&cmd=farther'
    }
  },
  created () { // 生命周期 created,获取数据
    (function (doc, win) { 
      var docEl = doc.documentElement,
        resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize',
        recalc = function () {
          var clientWidth = docEl.clientWidth;
          if (!clientWidth) return;
          docEl.style.fontSize = parseInt(100 * (clientWidth / 320) * 320 / 640,10) + 'px';
        };
      if (!doc.addEventListener) return; 
      doc.addEventListener('DOMContentLoaded', recalc, false);
    })(document, window);
    this.fetchData()
  },
  watch: {  // 观测变化,可以是值也可以是方法
  },
  methods: {
    fetchData () {
      const self = this  // 下面的 onload事件中 this 不再指向实例,所以要变量存一下  
      $.ajax({
        url : 'http://10.99.13.128:3000/t',
        type : 'get',
        data : {
          u : 'http://zy.cnhubei.com/m/dongxiang/news/list',
          d : JSON.stringify({
            psize : 20,
            rechid : '999999999999999999',
            infoid : null,
            cmd : 'farther'
          })
        },
        success : function(result){
          if(!result || !result.success){
            return;
          }

          self.list = result.data.data.list;
        },
        error : function(){},
        complete : function(){

        }
      });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.l-tit{
    text-align: center;
    padding: 0.6rem 0.6rem 0.3rem;
    font-size: 0.28rem;
    color: #333;
    background: #fff;
}
.l-tit:before {
    margin-right: 10px;
    transform: scale(1,.5);
    -webkit-transform: scale(1,.5);
}

.l-tit:after {
    margin-left: 10px;
    transform: scale(1,.5);
    -webkit-transform: scale(1,.5);
}

.l-tit:after, .l-tit:before {
    width: 40px;
    height: 1px;
    background: #bfbfbf;
    display: inline-block;
    content: '';
    vertical-align: middle;
}

</style>
