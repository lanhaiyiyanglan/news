<!-- Detail.vue -->  
<template>  
    <div class="detail">  
        <detail-header></detail-header>
        <div class="detailTxt">{{$route.params.info}}</div>
        <img :src="$route.params.img" alt=""> 
    </div>  
</template>  
<style>  
    .detail {  
        padding: 0.24rem;font-size:12px; 
    }  
    .detailTxt{font-size:14px;line-height:21px;}
    .detail img{width:100%;display:block;margin-top:0.2rem;}
</style>  
<script>  
    import DetailHeader from '../components/DetailHeader'  
    export default {   
        components: {  
            DetailHeader  
        }
    }  
</script>  