<template>
  <div class="bs-wrapper">
    <div class="bs-content">
      <DetailHead></DetailHead>
      <van-tabs v-model="active" animated sticky color="#fb000">
        <van-tab :title="'点餐'">
          <order></order>
        </van-tab>
        <van-tab :title="'评论'">
          <comment></comment>
        </van-tab>
        <van-tab :title="'商家'">商家页</van-tab>
      </van-tabs>
      <!-- {{$route.query.id}} -->
    </div>
  </div>
</template>

<script>
import DetailHead from "./DetailHead";
import Comment from "@/views/comment/index";
import Order from "@/views/order/index";
import BetterScroll from "better-scroll";
export default {
  data() {
    return {
      active: "0",
    };
  },
  components: {
    DetailHead,
    Comment,
    Order,
  },
  mounted() {
    setTimeout(() => {
      let bs = new BetterScroll(".bs-wrapper", {
        click: true,
        bounce: false,
      });
    }, 1000);
  },
};
</script>

<style lang="scss" scoped>
.bs-wrapper {
  height: 100vh;
}
</style>