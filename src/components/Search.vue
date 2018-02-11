<template>
  <div class="search-bar">
    <a class="table" href="javascript:void(0);" >
      <input class="search" type="text" placeholder="搜索专辑、声音">
      <i class="ic ic-search"></i>
    </a>
  </div>
</template>

<script>
export default {
  name: 'elNav',
  data () {
    return {
      menus: [
        {id: '999999999999999999', name: '热推'},
        {id: '652010202132123648', name: '要闻'},
        {id: '630903883975364608', name: '财经'},
        {id: '630903819802513408', name: '时事'},
        {id: '652010928770125824', name: '思想'},
        {id: '937891024376958976', name: '政法'},
        {id: '910779733736951808', name: '大学'},
        {id: '840031843238809600', name: '体育'},
        {id: '913561930915123200', name: '警讯'},
        {id: '814308033625853952', name: '香港'},
        {id: '630903954380951552', name: '悦读'},
        {id: '652011649053757440', name: '生活'},
        {id: '652278232246390784', name: '专题'}
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
      $.ajax({
        url : 'http://10.99.13.128:3000/t',
        type : 'get',
        data : {
          u : 'http://zy.cnhubei.com/m/dongxiang/news/list',
          d : JSON.stringify({
            psize : 20,
            rechid : self.currMenuId,
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
.search-bar {
  padding: 0.2rem;
  display: table;
  width: 100%;
  
  background: #f7f7f7;
  font-size: 0;
  box-sizing: border-box;
}
.search-bar .table{
  display: table;
  width: 100%;
  position: relative;
}

.search-bar .ic-search {
    background-image: url("https://s1.xmcdn.com/lib/openk/last/css/img/search-icon.png");
    background-repeat: no-repeat;
    background-size: 0.28rem 0.28rem;
    width:.6rem;
    height:.6rem;
    background-position:center center;
    position: absolute;
    left: 0;
    top: 0;

}


.search-bar .search {
  box-sizing: border-box;
  width: 100%;
  display: table-cell;
  background: #fff;
  color: #666;
  font-size: 0.24rem;
  padding: 0 0.1rem 0 0.6rem;
  margin: 0;
  height: 0.6rem;
  border-radius: 0.3rem;
  pointer-events: none;
  border: 1px solid #ccc;
}
</style>
