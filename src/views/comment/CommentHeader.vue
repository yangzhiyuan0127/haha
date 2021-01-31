<template>
    <div class="header-box">
    <div class="store-score">
        <div class="number">{{list.delivery}}</div>
        <div>商家评分</div>
    </div>
    <div class="score">
<div >口味<star :num="list.flavor"></star>  {{list.flavor}} 分</div>
  
<div>包装<star :num="list.packing"></star>   {{list.packing}}分</div>
    </div>
    <div class="xia-score">
        <div class="number">4.8</div>
        <div>配送评分</div>
    </div>
    </div>
</template>

<script>
import Star from '@/components/Star'
    export default {
          props:['list'],
         components:{
           Star
        }
    };
</script>

<style lang="scss" scoped>
   .header-box{
       display:flex;
       padding:0.3rem;
       .store-score,.xia-score{
           width: 1.86rem;
           text-align: center;
           font-size: 0.28rem;
           .number{
               font-size: 0.54rem;
               font-weight: 700;
               line-height: 0.54rem;
           }
       }
       .store-score{
           .number{
               color:#ffb000;
           }
       }
       .xia-score{
           .number{
               color:#999;
           }
       }
       .score{
           flex:1;
         
           }
       }
       
  
</style>