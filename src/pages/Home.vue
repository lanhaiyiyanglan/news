<template>
  <div>
    <Home-Header></Home-Header>  
    <div class="swiper-container">  
          <div class="swiper-wrapper">  
             <div class="swiper-slide" v-for="items in swiper" ><a href=""><img :src="items.activity.img"></a></div>  
          </div>  
          <div class="swiper-pagination"></div>  
    </div> 
    <UlList></UlList> 
  </div>
</template>

<script>
import Swiper from '../../static/js/swiper.min.js'
import HomeHeader from '../components/HomeHeader' 
import UlList from '../components/UlList' 
export default {  
  data(){  
    return {  
       swiper:[]   
    }    
  },
  components: {  
      HomeHeader,
      UlList
  }, 
  mounted(){  
      this.$http.get('http://www.vrserver.applinzi.com/aixianfeng/apihome.php').then((res) => {
                this.swiper=res.data.data.slide;  
                var mySwiper = new Swiper('.swiper-container', {  
                    autoplay: 2000,
                    pagination : '.swiper-pagination',  
                    paginationClickable :true,  
                    observer: true   
                })  
             }, (res) => {
                console.log('error');
      });
  }  
  
} 
</script>
<style>
 @import '../../static/css/swiper.min.css';
 body{background:#ffffff;}
 .swiper-container{width:100%;height:4.5rem;}
 .swiper-container img{width:100%;height:4.5rem;}
</style>