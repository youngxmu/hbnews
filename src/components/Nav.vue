<template>
  <div class="nav-wrapper">
    <ul class="nav">
      <li class="nav-item" v-for="menu in menus" v-bind:key="menu.id" v-on:click="selMenu(menu.id)" v-bind:style="menu.style" >{{ menu.name }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'elNav',
  data () {
    return {
      menus: [

        {id: '999999999999999999', name: '习近平讲话', style:{backgroundImage : 'url("http://fdfs.xmcdn.com/group38/M05/7F/7D/wKgJolpm5wHzQHRZAAArHnoBJM8170.png")'}},
        {id: '652010202132123648', name: '听党课', style:{backgroundImage : 'url("http://fdfs.xmcdn.com/group38/M05/7F/85/wKgJolpm5yHCu9h9AAAmXuaJDRw236.png")'}},
        {id: '630903883975364608', name: '学党规', style:{backgroundImage : 'url("http://fdfs.xmcdn.com/group38/M05/7F/7D/wKgJolpm5wHzQHRZAAArHnoBJM8170.png")'}},
        {id: '630903819802513408', name: '学党史', style:{backgroundImage : 'url("http://fdfs.xmcdn.com/group38/M05/7F/7D/wKgJolpm5wHzQHRZAAArHnoBJM8170.png")'}},
        {id: '652010928770125824', name: '党务问答', style:{backgroundImage : 'url("http://fdfs.xmcdn.com/group38/M05/7F/7D/wKgJolpm5wHzQHRZAAArHnoBJM8170.png")'}},
        {id: '937891024376958976', name: '经典品读', style:{backgroundImage : 'url("http://fdfs.xmcdn.com/group38/M05/7F/7D/wKgJolpm5wHzQHRZAAArHnoBJM8170.png")'}},
        {id: '910779733736951808', name: '智库观点', style:{backgroundImage : 'url("http://fdfs.xmcdn.com/group38/M05/7F/7D/wKgJolpm5wHzQHRZAAArHnoBJM8170.png")'}},
        {id: '840031843238809600', name: '经管创业', style:{backgroundImage : 'url("http://fdfs.xmcdn.com/group38/M05/7F/7D/wKgJolpm5wHzQHRZAAArHnoBJM8170.png")'}},
        {id: '913561930915123200', name: '故事汇', style:{backgroundImage : 'url("http://fdfs.xmcdn.com/group38/M05/7F/7D/wKgJolpm5wHzQHRZAAArHnoBJM8170.png")'}},
        {id: '652278232246390784', name: '声音', style:{backgroundImage : 'url("http://fdfs.xmcdn.com/group38/M05/7F/7D/wKgJolpm5wHzQHRZAAArHnoBJM8170.png")'}}
      ],
      currMenuId : '999999999999999999',
      branches: ['master', 'dev'],
      currentBranch: 'master',
      list: null,
      apiURL: 'http://zy.cnhubei.com/m/dongxiang/news/list?psize=20&rechid=999999999999999999&infoid=null&cmd=farther'
    }
  },
  created () { // 生命周期 created,获取数据
    // this.fetchData()
  },
  watch: {  // 观测变化,可以是值也可以是方法
    // currentBranch: 'fetchData'
  },
  methods: {
    fetchData () {
      const self = this  // 下面的 onload事件中 this 不再指向实例,所以要变量存一下  
      // $.ajax({
      //   url : 'http://10.99.13.128:3000/t',
      //   type : 'get',
      //   data : {
      //     u : 'http://zy.cnhubei.com/m/dongxiang/news/list',
      //     d : JSON.stringify({
      //       psize : 20,
      //       rechid : self.currMenuId,
      //       infoid : null,
      //       cmd : 'farther'
      //     })
      //   },
      //   success : function(result){
      //     if(!result || !result.success){
      //       return;
      //     }

      //     self.list = result.data.data.list;
      //   },
      //   error : function(){},
      //   complete : function(){

      //   }
      // });
    },
    selMenu : function(menuId){
      this.currMenuId = menuId;
      console.log(menuId);
      this.fetchData();
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.nav-wrapper {
  font-weight: normal;
  /*overflow: auto;*/
}
.nav-wrapper .nav {
  /*height:60px;
  line-height: 60px;*/
  /*height: .82rem; 
  line-height:0.82rem;
  background-color: #FFF;
  position: relative;
  color: #555555;
  width: auto;
  white-space: nowrap;
  */
  height: 2.4rem;
  padding : 0;
  margin:0;
  font-size: 0;
  padding: 0 0.1rem;
}
.nav-wrapper .nav li{
  background-size: auto 0.7rem;
  background-position: center top;
  background-repeat: no-repeat;
  list-style-type: none;
  padding: 0;
  display: inline-block;
  width: 1.2rem;
  height: 0.3rem;
  padding-top:0.8rem;
  text-align: center;
  vertical-align: top;
  font-size: .2rem; 
  float: left;
  margin-right: 0.05rem;
  margin-top: 0.2rem;
}
.nav-wrapper .nav li:nth-child(5n){
  margin-right: 0;
}
</style>
