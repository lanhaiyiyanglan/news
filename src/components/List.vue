<!-- List.vue -->  
<template>  
    <li class="sec_li">  
        <router-link class="lp_li_a" :to="{name:'Detail',query: {'id':id},params: {'id':id,'img':img,'info':info,'time':time}}"> 
            <dl> 
                <dt class="lp_li_imgWrap">  
                    <img :src="img" alt="">  
                </dt>
                <dd class="lp_li_imgTxt">  
                  <h2>{{ title }}</h2>  
                  <p class="lp_li_price">{{ total }}阅读<span>{{ time }}</span></p>
                </dd>
            </dl>
        </router-link>  
    </li>  
</template>  
  
<style scoped>  
.sec_li{padding:0.3rem;border-bottom:1px solid #ededed;}  
.sec_li dl{position:relative;display: -webkit-box;display: box;}
.sec_li  dl  dt{width:2.3rem;position: relative;margin-right:0.3rem;}
.sec_li  dl  dt img{display:block;width:100%;height:1.5rem;}
.sec_li  dl  dd{-webkit-box-flex: 1;box-flex: 1;display: box;display: -webkit-box;-webkit-box-orient: vertical;}
.sec_li  dl  dd h2{font-weight:normal;font-size: 16px;line-height: 24px;color:#333;display: -webkit-box;overflow: hidden;text-overflow: ellipsis;-webkit-line-clamp: 2;-webkit-box-orient: vertical;word-break: break-all;}
.sec_li  dl  dd p.lp_li_price{font-size:13px;color:#999;padding-top:5px;}
.sec_li  dl  dd p.lp_li_price span{float:right;font-size:12px;}
</style>  
  
<script>  
    export default {  
        props: ['id','total', 'title','img','info','time'],
    }  
</script>  