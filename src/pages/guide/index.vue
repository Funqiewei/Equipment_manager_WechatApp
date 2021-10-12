<template>
<div>
  <div class="title">
    1. 小程序服务简介
 </div>
    <div>
      <div class="sub">
      &nbsp;&nbsp;&nbsp;&nbsp;本服务为学生提供了远程预约服务，方便校友实时对设备进行预约选择。本小程序提供了两种使用设备途径：扫码立即使用、远程小程序预约。<br>
      
      </div>
  <br>
      <div class="title">
      2. 使用流程
      </div>
      <div class="sub">
      &nbsp;&nbsp;&nbsp;&nbsp;小程序使用流程简单易懂，只需要在"我的"页面中填写学号和姓名两步即可在"选择"中选择需要的时段实时预约设备，当然也可以直接去设备所在地用微信自带的"扫一扫"功能扫瞄设备显示的码进行实时使用未被预约设备。
      预约后在选择座位时会弹出头像授权，点击确认后再完成座位选择后点击"选好了"即完成预约，若是选择"现在就用"则会分配一台未被预约和使用的设备。
      <br><br>
      </div>
      <div  class="title">
      3. 管理预约
      </div>
      <div class="sub">
      &nbsp;&nbsp;&nbsp;&nbsp;在"列表"中，可以看到个人所有预约情况。可以按下取消按钮来进行取消预约设备。<br><br>
      </div>
      <div class="sub">
        &nbsp;&nbsp;&nbsp;&nbsp;从目前来看小程序设计的初衷是连接线上与线下。但将来，线上线下的融合模式，
      小程序势必在其中扮演极其重要的角色。<br>
      </div>
      <div class="sub">
      &nbsp;&nbsp;&nbsp;&nbsp;在场景化的思维方式下，用户将更注重自身使用体验，产品设计也将进一步贴合用户的实际倩况和消费习惯。<br>
      </div>

    </div>
  
  <van-toast id="van-toast"/>
</div>

</template>

<script>

import Toast from "vant-weapp/dist/toast/toast"
export default {
  data () {
    return {//日期
      
    }


  },

  methods: {
  },
        onLoad(){     
                Toast.loading({
                message: '加载中...',
                forbidClick: true,
                  });
          },
}
    


</script>

<style lang="scss" >
.title{
      font-size:32px;
      font-weight: 150;
      display:flex;
      justify-content: space-between;
    }
.sub{
      font-size:16px;
      font-weight: 150;
      
      justify-content: space-between;
      margin-top: 10px;
      margin-bottom: 10px;
    }





</style>
