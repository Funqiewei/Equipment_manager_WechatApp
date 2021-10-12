<template>
  <div>
      <van-tabs color="#3d7ef9"  :active="active" @change="onTabChange">
      <van-tab title="预约列表">
        <div v-show="!Appointment" class="title">
          还未预约任何设备
        </div>
        <div v-show="Appointment">
              <van-card 
                title-class="mytitle"
                thumb-class="myicon"
                desc-class="mydesc"
                :desc="describe"
                title="进行中"
                thumb="/static/images/seat_run.png"
              >
              <view slot="footer" class="mybutton">
              <van-button @click="onClickButton" size="mini">取消预约</van-button> 
              </view>
              </van-card>
        </div>

      </van-tab>
      <!--
      <van-tab title="已完成">
        <div v-if="AppointmentEND.status">
           <van-card 
                title-class="mytitle"
                thumb-class="myicon"
                desc-class="mydesc"
                :desc="describe"
                title="已完成"
                thumb="/static/images/slected_seat.png"
              />
        </div>
      </van-tab>-->
    </van-tabs>
    <van-toast id="van-toast"/>
    </div>

</template>

<script>
import Toast from "vant-weapp/dist/toast/toast"
export default {
  data () {
    return {
      active:'',
      describe:"启动时间:",
      Appointment:false,
      flag:0,
    }
  },
  methods:{
        onTabChange(event) {
         // wx.showToast({
         //   title: `切换完成`,
         // });
        },
        onChange(event) {
            var that = this
            that.activeNames=event.mp.detail
        },
        onClickButton(){
        var that=this
        that.Appointment=false
        this.globalData.Appointment=false
        that.flag=0
        that.describe="启动时间:"
        Toast.success("取消预约成功")
        //给后端发
        }
      },
      onShow(){
          var that=this
          if(this.globalData.Appointment&&that.flag==0){
            that.Appointment=this.globalData.Appointment
            if(this.globalData.timeSegment==1){
              that.describe=that.describe+this.globalData.month+"月"+this.globalData.day+"号"+"8:00"
            }
            if(this.globalData.timeSegment==2){
              that.describe=that.describe+this.globalData.month+"月"+this.globalData.day+"号"+"13:00"
            }
            if(this.globalData.timeSegment==3){
              that.describe=that.describe+this.globalData.month+"月"+this.globalData.day+"号"+"17:00"
            }
            console.log(this.globalData.Appointment,that.Appointment)
            that.flag=1
          }
          
      },
      onLoad(){     
        var that=this
        Toast.loading({
        message: '加载中...',
        forbidClick: true,
          });

        }
   

  };


</script>

<style lang="scss" >

.header {
  background-color:#fff ;
  border-radius: 0px 0px 5px 5px;
  display: flex;
  justify-content: space-around;
  padding: 0 8px;
  box-shadow: #d6d6d6 0px 0px 5px;
  height: 100px;
  overflow: hidden;
  background-color: #fff;
}

.mytitle{
  position:absolute;
  color:#3d7ef9;
  top: 10px;
  right:50px
}

.mydesc{
  position:absolute;
  color:#3d7ef9;
  right:50px;
  bottom:35px;
}
.mybutton{
  position:absolute;
  color:#3d7ef9;
  right:60px;
  bottom:10px;
}
.title{
  font-size:16px;
      font-weight: 150;
      margin-top: 50px;
      margin-bottom: 10px;
      text-align:center
}
.myicon{
width: 15vw !important;
height: 15vw !important;
margin-left: 50px;
}

</style>
