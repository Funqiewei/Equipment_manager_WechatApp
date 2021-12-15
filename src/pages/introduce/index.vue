<template>
  <div>
   <div>
     项目介绍
   </div>
    <van-toast id="van-toast" />
  </div>
</template>

<script>
import Toast from "vant-weapp/dist/toast/toast";
export default {
  data() {
    return {
      //日期
    };
  },

  methods: {},
  onShow() {
    Toast.loading({
      message: "加载中...",
      forbidClick: true,
      duration: 500,
    });
  },
};
</script>

<style lang="scss" >

</style>
