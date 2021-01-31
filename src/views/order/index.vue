<template>
  <div class="order-container">
    <!-- 左侧的分类 -->
    <div class="cate-box">
      <ul>
        <li :class="{active: index==currentIndex,'cate-list':true}" v-for="(obj, index) in nav" @click="change(index)" :key="obj.id">
          {{ obj.name }}
        </li>
      </ul>
    </div>
    <!-- 右侧商品 -->
    <div class="pro-box">
      <div>
        <div class="prod-cate-box" v-for="(obj, index) in goods" :key="index">
          <h2>{{ obj.name }}</h2>
          <ul>
            <li class="prod-list" v-for="prod in obj.content" :key="prod.id">
              <img class="prod-img" :src="prod.img" alt="" />
              <p>{{ prod.name }}</p>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import BetterScroll from "better-scroll";
export default {
  data() {
    return {
      nav: [],
      goods: [],
      currentIndex:0,//记录当前激活索引
      scrollY:0,//prodScroll滚动的高度
      pos:[]//记录所有分类div的位置
    };
  },
  methods: {
    change(index) {
      let prodCateList = document.getElementsByClassName("prod-cate-box");
      console.log(prodCateList[index]);

    this.prodScroll.scrollToElement(prodCateList[index], 300);
    this.currentIndex=index;
    },

    getPos(){
      let prodCateList = document.getElementsByClassName("prod-cate-box");
          let H = 0;
      for(let i=0; i<prodCateList.length; i++){
        if(i == 0){
          this.pos.push(0)
        }else{
          H += prodCateList[i-1].offsetHeight;
          this.pos.push(H);
        }
      }
      console.log(this.pos)
    }
  },
  created() {
    axios
      .get(
        `http://admin.gxxmglzx.com/tender/test/get_nav?id=${this.$route.query.id}`
      )

      .then((res) => {
        console.log(res.data.data);
        this.nav = res.data.data.nav;
        this.goods = res.data.data.goods;

        //渲染到页面后
        this.$nextTick(() => {
          this.cateScroll = new BetterScroll(".cate-box", {
            bounce: false,
          });
          //   console.log(2222222222222)
          this.prodScroll = new BetterScroll(".pro-box", {
            bounce: false,
            probeType:3
          });
          this.prodScroll.on("scroll",position =>{
           // console.log(position.x, position.y);
           this.scrollY=Math.abs(position.y)
           console.log(this.scrollY)
          });
          //计算每个分类位置
        this.getPos();
        });
      });

    //等待数据回来
  },
  watch:{
    scrollY(val){
     // console.log(val)
      //判断val在哪个坐标范围内
      for(let index=0; index < this.pos.length;index++ ){
        let pos1=this.pos[index];
        let pos2=this.pos[index+1];
        if(val>=pos1&&val <pos2){
          console.log(index);
          this.currentIndex=index;
          let cateList=document.querySelectorAll('.cate-list');
          this.cateScroll.scrollToElement(cateList[index],300)
          break;
        }
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.order-container {
  display: flex;
  padding-bottom: 50px;
  .cate-box {
    //视口高度-上44-下50
    height: calc(100vh - 94px);
    flex: 1;
    li {
      padding: 0.18rem 0.24rem 0.44rem;
      background-color: #f5f5f5;
      &.active{
        color: red;
      }
    }
  }
  .pro-box {
    flex: 3;
    height: calc(100vh - 94px);
    .prod-list {
      display: flex;
      .prod-img {
        width: 1.5rem;
      }
      p {
        flex: 1;
      }
    }
  }
}
</style>