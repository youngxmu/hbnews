<template>
<div class="list-wrapper">
  <elNav></elNav>
  <ul class="news-list">
    <li class="news-desc normal" v-for="news in list">
      <a :href="news.shareurl" :title="news.title">
        <div class="pic">                       
           <img :src="news.pics[0].u ">
        </div> 
        <div class="title"><span>{{ news.title }}</span></div>
        <div class="info">
          <span class="news-type none"></span>
          <span class="news-date">今日</span>
        </div>
      </a>
    </li>
  </ul>
</div>
</template>
<script>
import elNav from '@/components/Nav.vue'
export default {
  name: 'news-list',
  components: {
    elNav
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
ul{
  margin: 0;
  padding: 0;
}
li{
  list-style-type: none;
}

a{
  color: #333333;
}
.news-list{
  /*margin-top: 0.82rem;*/
}
.news-list>.title{background: #e7e7e7;color: #898989;height: 0.6rem;line-height: 0.6rem;font-size: 0.3rem;padding-left: 0.2rem;
 }
.news-list>.title .count{margin-right: 0.36rem;}
.news-list>.title .count .news-index{color: #fe5200;font-size: 1.1em;font-style: normal;}


.news-list .news-desc{padding: 0.2rem;border-bottom: 1px solid #dddddd;position: relative;box-sizing:border-box;}
.news-list .news-desc:last-child{border: none ;}/*!important*/
.news-list .news-desc .pic{width: 1.82rem;height: 1.32rem;float: left;}
.news-list .news-desc .pic img{width: 100%;height: 100%;object-fit:cover;}
.news-list .news-desc .title{
    box-sizing: border-box;
    margin: 0 0 0.1rem 0;
    /*margin: 0;*/
    width: 100%;font-size: 0.36rem;text-align: justify;line-height: 0.44rem;max-height: 0.88rem;overflow: hidden;
}
.news-list .news-desc .info{
    box-sizing: border-box;
    line-height: 0.36rem;
    height: 0.36rem;
    font-size: 0.24rem;
    color: #999999;width: 100%;
    margin-top: 0.1rem;
    text-align: left;
}
.news-list .news-desc .info .news-date{display: inline-block;}
.news-list .news-desc .info .page-view{float: right;}

.news-list .news-desc.normal{height: 1.8rem;}
.news-list .news-desc.normal .pic{}
.news-list .news-desc.normal .title{
    position: absolute;
    top: 0;
    left: 0;
    padding: 0 0.2rem 0 2.2rem;
    margin-top: .2rem;
}
.news-list .news-desc.normal .info{
    position: absolute;
    bottom: 0.2rem;
    left: 0;
    padding: 0 0.2rem 0 2.2rem;
}


.news-list .news-desc.text{}
.news-list .news-desc.text .pic{display:none;}
.news-list .news-desc.text .title{
    position: relative;
    box-sizing: border-box;
    padding: 0 0 0.1rem 0;
    margin: 0;
    width: 100%;font-size: 0.36rem;text-align: justify;line-height: 0.44rem;height: 0.98rem;overflow: hidden;
}
.news-list .news-desc.text .info{}

.news-list .news-desc.big-img{}
.news-list .news-desc.big-img .pic{width: 100%;height: 2.36rem;float: none;}
.news-list .news-desc.big-img .pic img{width: 100%;height: 100%;object-fit:cover;}
.news-list .news-desc.big-img .title{
  /*position: relative;
  box-sizing: border-box;
  padding: 0 0 0.1rem 0;
  margin: 0;
  width: 100%;font-size: 0.36rem;text-align: justify;line-height: 0.44rem;height: 0.54rem;*/
}
.news-list .news-desc.big-img .info{}

.news-list .news-desc.gallery{}
.news-list .news-desc.gallery .pic{width: 100%;height: 1.6rem;text-align: justify;float: none;font-size: 0;}
.news-list .news-desc.gallery .pic img{width: 32%;height: 1.6rem;object-fit:cover;margin-right: 2%;}
.news-list .news-desc.gallery .pic img:last-child{margin-right: 0;}
.news-list .news-desc.gallery .title{
  /*position: relative;
  box-sizing: border-box;
  padding: 0 0 0.1rem 0;
  margin: 0;
  width: 100%;font-size: 0.36rem;line-height: 0.44rem;height: 0.64rem;*/
}

.news-list .news-desc.gallery .info{
}



.news-list .news-desc.video{}
.news-list .news-desc.video .pic{width: 100%;height: 4rem;float: none;position: relative;}
.news-list .news-desc.video .pic img{width: 100%;height: 100%;object-fit:cover;}
.news-list .news-desc.video .title{}
.news-list .news-desc.video .info{}
.news-list .news-desc.video .video-play{
  width: 100%;
  height: 100%;
  position: absolute;
  left: 0;
  top: 0;
  /*background-image: url("../img/player_play.png?__sprite");*/
    background-repeat: no-repeat;
    background-position: center center;background-size: 0.98rem 0.98rem;
}

.news-list .news-desc.video .info .video-time{
    /*background-image: url("../img/f-time.png?__sprite");*/
    background-repeat: no-repeat;
    background-position: left center;
    background-size: 0.34rem 0.34rem;
    padding-left: 0.44rem;
    margin-right: 0.1rem;
    height: 0.36rem;
    line-height: 0.36rem;
    display: inline-block;

}
.news-list .news-desc.video .info .play-count{
    /*background-image: url("../img/f-video.png?__sprite");*/
    background-repeat: no-repeat;
    background-position: left center;
    background-size: 0.34rem 0.34rem;
    padding-left: 0.44rem;
    margin-right: 0.1rem;
    height: 0.36rem;
    line-height: 0.36rem;
    display: inline-block;
}
.news-list .news-desc.video .info .video-live{
    height: 0.36rem;
    line-height: 0.36rem;
    display: inline-block;
    color: #fe5200;
    vertical-align: top;
    margin-left: -0.15rem;
}


</style>
