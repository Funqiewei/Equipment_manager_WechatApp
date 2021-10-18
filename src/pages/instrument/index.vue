<template>
 
<div>
  <van-toast id="van-toast"/>
          <div class="header">
            <div class="seatStatusList">
                <img class="statusLabel" src="/static/images/seat_abled.png">
                <span>可选用</span>
                <span >&nbsp;</span>
                <img class="statusLabel" src="/static/images/slected_seat.png">
                <span>已选中</span>
                <span >&nbsp;</span>
                <img class="statusLabel" src="/static/images/seat_used.png">
                <span>不可选</span>
                <span >&nbsp;</span>
              </div>
          </div>


      <div class="body">
              <div class="chooseseatStatusList"  >
              <img class="statusLabel"  @click="onClickseat('0')"  v-show="Seatflag[0]=='0'" src="/static/images/seat_abled.png">
              <img class="statusLabel"    v-show="Seatflag[0]=='2'" src="/static/images/seat_used.png">
              <img  class="statusLabel"  v-show="Seatflag[0]=='1'" src="/static/images/slected_seat.png"  >
              <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>

              <img class="statusLabel"  @click="onClickseat('1')"  v-show="Seatflag[1]=='0'" src="/static/images/seat_abled.png">
              <img class="statusLabel"    v-show="Seatflag[1]=='2'" src="/static/images/seat_used.png">
               <img  class="statusLabel"  v-show="Seatflag[1]=='1'" src="/static/images/slected_seat.png"  >
              <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>

              <img class="statusLabel"  @click="onClickseat('2')" v-show="Seatflag[2]=='0'" src="/static/images/seat_abled.png">
              <img class="statusLabel"    v-show="Seatflag[2]=='2'" src="/static/images/seat_used.png">
               <img  class="statusLabel"  v-show="Seatflag[2]=='1'" src="/static/images/slected_seat.png"  >
              <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>

              <img class="statusLabel"  @click="onClickseat('3')"  v-show="Seatflag[3]=='0'" src="/static/images/seat_abled.png">
              <img class="statusLabel"    v-show="Seatflag[3]=='2'" src="/static/images/seat_used.png">
              <img  class="statusLabel"  v-show="Seatflag[3]=='1'" src="/static/images/slected_seat.png"  >
              <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
              </div>
            
              <div class="chooseseatStatusList"  >
              <img class="statusLabel"  @click="onClickseat('4')"  v-show="Seatflag[4]=='0'" src="/static/images/seat_abled.png">
              <img class="statusLabel"    v-show="Seatflag[4]=='2'" src="/static/images/seat_used.png">
               <img  class="statusLabel" @click="onClickseat('4')" v-show="Seatflag[4]=='1'" src="/static/images/slected_seat.png"  >

              <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
              <img class="statusLabel"  @click="onClickseat('5')" v-show="Seatflag[5]=='0'" src="/static/images/seat_abled.png">
              <img class="statusLabel"    v-show="Seatflag[5]=='2'" src="/static/images/seat_used.png">
              <img  class="statusLabel"  v-show="Seatflag[5]=='1'" src="/static/images/slected_seat.png"  >

              <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
              <img class="statusLabel"  @click="onClickseat('6')"  v-show="Seatflag[6]=='0'" src="/static/images/seat_abled.png">
              <img class="statusLabel"    v-show="Seatflag[6]=='2'" src="/static/images/seat_used.png">
              <img  class="statusLabel"  v-show="Seatflag[6]=='1'" src="/static/images/slected_seat.png"  >

              <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
              <img class="statusLabel"  @click="onClickseat('7')"  v-show="Seatflag[7]=='0'" src="/static/images/seat_abled.png">
              <img class="statusLabel"    v-show="Seatflag[7]=='2'" src="/static/images/seat_used.png">
              <img  class="statusLabel"  v-show="Seatflag[7]=='1'" src="/static/images/slected_seat.png"  >
              <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
              </div>
            
              <div class="chooseseatStatusList"  >
              <img class="statusLabel"  @click="onClickseat('8')" v-show="Seatflag[8]=='0'" src="/static/images/seat_abled.png">
              <img class="statusLabel"    v-show="Seatflag[8]=='2'" src="/static/images/seat_used.png">
              <img  class="statusLabel"  v-show="Seatflag[8]=='1'" src="/static/images/slected_seat.png"  >
              <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
              <img class="statusLabel"  @click="onClickseat('9')"  v-show="Seatflag[9]=='0'" src="/static/images/seat_abled.png">
              <img class="statusLabel"    v-show="Seatflag[9]=='2'" src="/static/images/seat_used.png">
              <img  class="statusLabel"  v-show="Seatflag[9]=='1'" src="/static/images/slected_seat.png"  >

              <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
              <img class="statusLabel"  @click="onClickseat('10')"  v-show="Seatflag[10]=='0'" src="/static/images/seat_abled.png">
              <img class="statusLabel"    v-show="Seatflag[10]=='2'" src="/static/images/seat_used.png">
              <img  class="statusLabel"  v-show="Seatflag[10]=='1'" src="/static/images/slected_seat.png"  >

              <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
              <img class="statusLabel"  @click="onClickseat('11')" v-show="Seatflag[11]=='0'" src="/static/images/seat_abled.png">
              <img class="statusLabel"    v-show="Seatflag[11]=='2'" src="/static/images/seat_used.png">
              <img  class="statusLabel"  v-show="Seatflag[11]=='1'" src="/static/images/slected_seat.png"  >
              <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
              </div>
  
              <div class="chooseseatStatusList"  >
              <img class="statusLabel"  @click="onClickseat('12')"  v-show="Seatflag[12]=='0'" src="/static/images/seat_abled.png">
              <img class="statusLabel"    v-show="Seatflag[12]=='2'" src="/static/images/seat_used.png">
              <img  class="statusLabel" @click="onClickseat('12')" v-show="Seatflag[12]=='1'" src="/static/images/slected_seat.png"  >

              <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
              <img class="statusLabel"  @click="onClickseat('13')"  v-show="Seatflag[13]=='0'" src="/static/images/seat_abled.png">
              <img class="statusLabel"    v-show="Seatflag[13]=='2'" src="/static/images/seat_used.png">
              <img  class="statusLabel"  v-show="Seatflag[13]=='1'" src="/static/images/slected_seat.png"  >

              <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
              <img class="statusLabel"  @click="onClickseat('14')" v-show="Seatflag[14]=='0'" src="/static/images/seat_abled.png">
              <img class="statusLabel"    v-show="Seatflag[14]=='2'" src="/static/images/seat_used.png">
              <img  class="statusLabel" v-show="Seatflag[14]=='1'" src="/static/images/slected_seat.png"  >
              <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
              </div>
          </div>  
      
            
            <div class="button1">
              <van-button 
                plain 
                size="normal"
                color="#3d7ef9"
                type="primary"
                block 
                @click="onClickButton1"
               >选好了<image class='btnImg' src='/static/images/run.png'></image>
               </van-button>
               </div>
      </div> 
</template>

<script>
import Vue from 'vue' 
import { connect } from "mqtt/dist/mqtt.js";
const date=''
const timeSegment=''
import Toast from "vant-weapp/dist/toast/toast"
// Toast.setDefaultOptions({ duration: 1000 });
const mqttUrl = 'wxs://mqtt.emqttedu.xyz:8084/mqtt'
export default {
  data () {
    return {
      Seatflag:['0','0','0','0','2','2','2','2','2','2','2','2','2','2','2'],
      Selectnum:'100',
      id:'0',
      userID:"",
      userName:"",
      isshow:false,
      show: false,
      Appointment:false,
      userInfo: {},
      hasUserInfo: false,
      canIUseGetUserProfile: false,
      data:'',
      avatar:'',
      imgUrls: [
          '/static/images/seat_abled.png',
          '/static/images/seat_used.png',
          "/static/images/slected_seat.png"
          ]
    }
  },
  methods:{
    onClickseat:function(id){
            var that=this 
            if(!that.avatar){
                  wx.getStorage({
                  key: 'avatar',
                  success (res) {
                    that.avatar=res.data.storageavatar
                  },
                  fail()
                  {that.avatar='0'}
                })
                }
                  wx.getStorage({
                    key: 'Name',
                    success (res) {
                      that.userName=res.data.storageName
                    },
                  })
                  wx.getStorage({
                    key: 'ID',
                    success (res) {
                      that.userID=res.data.storageID
                    },
                  })
            
            if(!that.avatar){
               wx.getUserProfile({
                    desc: '用于预约机器的头像显示', // 声明获取用户个人信息后的用途，后续会展示在弹窗中，请谨慎填写
                    success(res){     
                        that.userInfo=res.userInfo,
                        that.hasUserInfo= true
                        that.avatar=that.userInfo.avatarUrl
                        console.log(that.avatar);
                    },
            })
            {     
              wx.setStorage({
                  key:"avatar",
                  data:{
                    storageavatar:that.avatar,
                  },
                  success (res) {
                    console.log(res);
                    console.log("储存成功！")
                    },
                  fail (res) {
                    console.log(res)
                    console.log("储存失败！")
                  }
                });
              }
            };

           //console.log(that.avatar)
            for (let index = 0; index < that.Seatflag.length; index++) {
                  if((that.Seatflag[index]=='1')){
                    that.$set(that.Seatflag,index,'0')
                    break;
                }
            }

             if(that.Seatflag[id]=='0'){
                 that.$set(that.Seatflag,id,'1')
                 that.Selectnum=id
                // console.log(that.Selectnum)
            }
            console.log(that.Selectnum,id,"座位被点击了")
          
        },
        
      onClickButton1(){
        let that =this
          //console.log(event,"按钮被点击了")
         //that.client.publish('/mysmarthome/sub','按钮按下')
         //预约
        if(this.globalData.Appointment){
                Toast.fail('预约完成后再进行预约');
        }
         else if((!that.userName)&&(!that.userID)){
              Toast.fail('完善学号或姓名');
         }
         else if(that.Selectnum=='100'){
              Toast.fail('未选中座位');
         }else{
         
            this.globalData.timeSegment=that.timeSegment
            this.globalData.Appointment=true
            this.globalData.Selectnum=that.Selectnum
            this.globalData.month=that.month
            this.globalData.day=that.day
            that.Appointment=this.globalData.Appointment
            console.log(that.avatar)
            console.log("当前学号：",that.userID)
            console.log("预约成功：",this.globalData.Appointment)
            console.log("姓名：",that.userName)
            console.log("选择机号"+that.Selectnum)
            console.log(that.month+"月   "+that.day+"号   "+"选择时段"+that.timeSegment)//可以打印一下option看查看参数
            wx.setStorage({
                  key:"appointment",
                  data:{
                    storagetimeSegment:that.timeSegment,
                    storageAppointment:that.Appointment,
                    storagemonth:that.month,
                    storageday:that.day,
                  },
                  success (res) {
                    console.log(res);
                    console.log("储存预约信息成功！")
                    },
                  fail (res) {
                    console.log(res)
                    console.log("储存预约信息失败！")
                  }
                }); 
            wx.switchTab({url:"/pages/list/main"})
         }
         
             wx.request({
              url: 'test.php', //仅为示例，并非真实的接口地址
              data: {
                x: '',
                y: ''
              },
              header: {
                'content-type': 'application/json' // 默认值
              },
              success (res) {
                console.log(res.data)
              }
            })
            
      },
  },

onShow(){     
          var that=this
          Toast.loading({
          message: '加载中...',
          forbidClick: true,
            });

},
            

onLoad: function (option) {
   var that =this
　　console.log(option)//可以打印一下option看查看参数
    that.month=option.month
    that.day=option.day
    that.timeSegment=option.timeSegment
    if (wx.getUserProfile) {
        that.canIUseGetUserProfile=true
    }     
    //console.log(that.date+"    "+that.timeSegment)//可以打印一下option看查看参数
    /*wx.request({
          url: 'test.php', //仅为示例，并非真实的接口地址
          data: {
            x: '',
            y: ''
          },
          header: {
            'content-type': 'application/json' // 默认值
          },
          success (res) {
            console.log(res.data)
          }
        })*/
  }
}

</script>

<style lang="scss"scoped>
.seatStatusList {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100px;
}
.btnImg {
  width: 50rpx;
  height: 50rpx;
  position: absolute;
  left: 30px;
  margin-top: 10px;
}
.chooseseatStatusList {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100px;
  margin-top: 2px;
  margin-left: 10px;
}

.statusLabel{
  margin-top: 36px;
  margin-bottom: 36px;
  width:50px;
  height:50px;
  
}
.page {
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  color: #999;
}
.header {
  display: flex;
  height: 100px;
  padding: 0 8px;
  overflow: hidden;
  background-color:#fff ;
  border-radius: 0px 0px 10px 10px;
  border: 2rpx solid #3d7ef9;
  justify-content: space-around;
  box-shadow: #d6d6d6 0px 0px 5px;
  
  background-color: #fff;
}
.body{
  background-color: #fff;
}
.main {
  background-color: #eee;
  flex-grow: 1;
  overflow: hidden;
}
.footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 1.2rem;
  background-color: #fff;
}
.mrgR60 {
  margin-right: 0.6rem;
}

.button1{
  margin: 0 auto;
  width: 50%;
  position:fixed;
  bottom: 50px;
  left:0px;
  right:0px;
}


.data-wrapper{
      margin-top: 20px;
      display: flex;
      justify-content: space-between;
      .data{
        background-color: #fff;
        width: 150px;
        height:80px;
        border-radius: 20px;
        display: flex;
        justify-content: space-around;
        padding: 0 8px;
        box-shadow: #d6d6d6 0px 0px 5px;
        .data-logo{
          height: 36px;
          width: 36px;
          margin-top: 15px;
        }
        .data-text{
           margin-top: 15px;
           columns: #7f7f7f; ;
           .data-title{
             text-align:middle;
           }
           .data-value{
             font-size: 26px;
           }
        }
      }
  }



</style>
