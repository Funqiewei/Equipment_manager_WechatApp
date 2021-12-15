<template>
  <div>
    <div class="title">1. 小程序服务简介</div>
    <div>
      <div class="sub">
        &nbsp;&nbsp;&nbsp;&nbsp;本服务为学生提供了远程预约服务，方便校友实时对设备进行预约选择。提供了以下使用设备途径：线下立即使用、小程序预约、Web预约使用。<br />
      </div>
      <br />
      <div class="title">2. 使用流程</div>
      <div class="sub">
        &nbsp;&nbsp;&nbsp;&nbsp;小程序使用流程简单易懂，登录或注册好后，只需要在"选择"页面中选择中选择需要的时段进行跳转到实时预约设备页面，再完成座位选择后点击"选好了"即完成预约，若是选择"现在就用"无需选择所用的时间。
        <br /><br />
      </div>
      <div class="title">3. 管理预约</div>
      <div class="sub">
        &nbsp;&nbsp;&nbsp;&nbsp;在"列表"中，可以看到个人所有预约情况。可以按下取消按钮来进行取消预约设备。<br /><br />
      </div>
      <div class="sub">
        &nbsp;&nbsp;&nbsp;&nbsp;从目前来看小程序设计的初衷是连接线上与线下。但将来，线上线下的融合模式，
        小程序势必在其中扮演极其重要的角色。<br />
      </div>
      <div class="sub">
        &nbsp;&nbsp;&nbsp;&nbsp;在场景化的思维方式下，用户将更注重自身使用体验，产品设计也将进一步贴合用户的实际倩况和消费习惯。<br />
      </div>
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
.title {
  font-size: 32px;
  font-weight: 150;
  display: flex;
  justify-content: space-between;
}
.sub {
  font-size: 16px;
  font-weight: 150;

  justify-content: space-between;
  margin-top: 10px;
  margin-bottom: 10px;
}
</style>
