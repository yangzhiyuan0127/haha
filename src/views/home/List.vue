<template>
    <div>
<ul class="store-list-box">
    <li class="store-list" v-for="obj in list" :key="obj.id"
      @click="$router.push({path:'/detail',query:{id:obj.id}})">
        <img class="store-img" :src="obj.img" alt="">
         <div class="store-info">
             <h2>{{obj.name}}</h2>
             <div>
                 <star num="3"></star>
                 {{obj.num}}</div>
             <div>配送时间：{{obj.minute}}</div>
         </div>
    </li>
</ul> 
<img class="loading" v-show="isShow" src="@/assets/images/loading.gif" alt="">
    </div>
</template>
<script>
import axios from 'axios'
import Star from '@/components/Star'
    export default {
        data(){
            return{
                list:[],
                Num:0,
                isShow:true,
                isFinished:false
            }
        },
        components:{
          Star
        },
        methods:{
     getData(){
      axios.get("http://admin.gxxmglzx.com/tender/test/get_store?current="+this.Num+"&size=10")
     .then((res)=>{
       // console.log(res.data.data.list);
        this.list= [...this.list,...res.data.data.list]
        this.Num++;
        this.isShow=false;
        if(res.list.length=res.data.data.tolal){
         this.isFinished=true
        }
    }).catch((err)=>{
        console.log(err); 
            })  
        }
    },
        //获取列表的数据
    created(){

        this.getData()

        window.onscroll=() =>{
            let scrollTtop=document.documentElement.scrollTop;
            let clientHeight=document.documentElement.clientHeight;
            let scrollHeight=document.documentElement.scrollHeight;
        if(scrollTtop+clientHeight==scrollHeight ){
      
      this.isShow=true;
      
      this.getData();
                }
            }
        }
    };
</script>

<style lang="scss" scoped>
.store-list-box{
    padding: 0.2rem;
   .store-list{
       //父元素flex子元素横置
       display: flex;
       .store-img{
           width:1.2rem;
       }
    .store-info{
        flex:1;
    }
   }
}
.loading{
    position: fixed;
    left:50%;
    top:50%;
    transform: translate(-50%,-50%);
    width:1.2rem;
    height:1.2rem;
}
</style>