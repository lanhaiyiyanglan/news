<!-- UlList.vue -->  
<template>  
      <div id="scrollMore">
        <ul class="cont_ul">  
            <List  
                v-for="item in listdata" 
                :id="item.id"
                :total="item.total"  
                :title="item.title"
                :img="item.img"
                :info="item.info"
                :time="item.time">  
            </List> 
            <div v-if="isShow" id="loading">
              <img src="../assets/loading.gif">
            </div>
        </ul>   
      </div> 
</template>  
<style>   
  .content{}
</style>  
<script>  
    import List from '../components/List' 
    export default {  
        data () {  
            return {  
                isShow:false,
                counter : 1, //默认已经显示出5条数据 count等于一是让从6条开始加载
                num : 5,  // 一次显示多少条
                pageStart : 0, // 开始页数
                pageEnd : 0, // 结束页数
                listdata: [], // 下拉更新数据存放数组
            }  
        },  
        // 在components字段中，包含导入的子组件  
        components: {
            List
        },
        mounted : function(){
              this.getList();
              var _self=this;    
              var tagId = "scrollMore";
              var pressX = 0,pressY = 0;
              var obj = document.getElementById(tagId);
              obj.addEventListener('touchmove', function(event) {}, false);
              obj.addEventListener('touchstart', function(event) {
                  if (event.targetTouches.length == 1) {
                      var touch = event.targetTouches[0];
                      pressX = touch.pageX;
                      pressY = touch.pageY;
                  }
              }, false);
              obj.addEventListener('touchend', function(event) {
                  if (event.targetTouches.length == 1) {
                      var touch = event.targetTouches[0];touchend.value = touch.pageX + ';' + touch.pageY;
                  }
                  if (document.body.scrollTop+screen.height+20>document.body.scrollHeight) {
                    _self.loadMore();
                  }
              }, false);
        },
        methods: {
            getList(){
              let vm = this;
              vm.$http.get('/api/books').then((res) => {
                       vm.listdata = res.data.data.slice(0,5);
                     }, (res) => {
                        console.log('error');
              });
        },
        loadMore: function() {
                  let vm = this;
                  vm.$http.get('/api/books').then((res) => {
                      vm.counter++;
                      vm.pageEnd = vm.num * vm.counter;//翻页数*当前页值 5*2=10
                      vm.pageStart = vm.pageEnd - vm.num;//翻页后的末尾页值-翻页值10-5=5
                      vm.isShow=true;
                      let arr=res.data.data;
                      let i = vm.pageStart;//5
                      let end = vm.pageEnd;//10
                      if(end<=res.data.data.length){
                            for(; i<end; i++){
                              let obj ={
                                id:'',
                                total:'',
                                title:'',
                                img:'',
                                info:'',
                                time:''
                              };
                              obj["id"] = arr[i].id;
                              obj["total"] = arr[i].total;
                              obj["title"] = arr[i].title;
                              obj["img"] = arr[i].img;
                              obj["info"] = arr[i].info;
                              obj["time"] = arr[i].time;
                              vm.listdata.push(obj);
                            }
                      }else{
                        if(this.$el.querySelector('#loading').children.length>=1){
                          this.$el.querySelector('#loading img').style.display = 'none';
                        }
                        this.$el.querySelector('#loading').innerHTML = '别拖了，没有啦！';
                      } 
                     }, (res) => {
                        console.log('error');
                    });
        }
      }
}  
</script>  
<style>
#scrollMore{}
#loading{text-align:center;font-size:14px;color:red;}
</style>