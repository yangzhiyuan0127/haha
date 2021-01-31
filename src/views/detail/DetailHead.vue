<template>
    <div class="container">
     <div class="back">&lt;</div>
     <div class="store-info">
         <img class="store-img" src="" alt="">
         <div class="store-msg">
             <div class="detail">
                 aaa
             </div>
         </div>
     </div>
    </div>
</template>

<script> 
    export default {
        
    }
</script>

<style lang="scss" scoped>
.container{
    background: #2e2f3b;
    color: #fff;
    padding:0.2rem;
    .back{
        font-size:20px;
        margin-bottom:0.2rem;
    }
    .store-info{
        display:flex;
        .store-img{
            width:1.7rem;
            
        }
        .store-msg{
            flex:1;
            width: 0;
            .detail{
                overflow: hidden;
                text-overflow: ellipsis;
                white-space: nowrap; //不换行
              
            }
        }
    }
}
</style>