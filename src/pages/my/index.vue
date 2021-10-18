<template>
<div>
  <!--
  <div class="headerPic">

  </div>-->
   <div class="wrapper">
    <!-- 个人资料 -->
    <div class="profile">
      
      <div class="meta">
        <!-- <image class="avatar" src="http://static.botue.com/ugo/uploads/monkey.png"></image> -->
        <open-data class="avatar" type="userAvatarUrl"></open-data>
        <!-- <text class="nickname">nickname</text> -->
        <open-data class="nickname" type="userNickName"></open-data>
      </div>
    </div>
        
        <!-- <van-field 
          label="学号"
          placeholder="请输入学号"
          :value="inputID"
          @change="onIDChange"
          input-class="right"
          />

          <van-field 
          label="姓名"
          placeholder="请输入姓名"
          :value="inputName"
          @change="onNameChange"
          input-class="right"
          /> -->

          <div class="margin">
           <van-cell title="小程序版本" value="1.0.0x" />
          </div>
          <div class="margin">
        <van-cell @click="clickguide" title="使用指南" value=" " />
          </div>
        <!-- 其它 -->
          <div class="margin">
        <van-cell @click="clickhistory" title="当前设备" value=" " />
          </div>

          
    
      
    

  </div>
<van-toast id="van-toast" />
</div>

</template>

<script>
import Toast from "vant-weapp/dist/toast/toast"
export default {
  data () {
    return {
     inputID:"",
     inputName:"",
    }


  },
  methods:{

    clickguide(){
      const url ="/pages/guide/main"
      wx.navigateTo({ url })
    },

    clickhistory(){
      const url ="/pages/list/main"
      wx.switchTab({ url })
    },

    onNameChange(event){
    var that=this  
    that.$set(that,"inputName",event.mp.detail)
    //console.log("当前姓名：",event.mp.detail)
    this.globalData.Name =event.mp.detail
    console.log("当前学号：",this.globalData.Name)

      wx.setStorage({
        key:"Name",
        data:{
          storageName:that.inputName,
        },
        success (res) {
          console.log(res);
          console.log("储存姓名成功！")
          },
        fail (res) {
          console.log(res)
          //console.log("储存姓名失败！")
        }
      });
        },

      onIDChange(event){
          var that=this  
          that.$set(that,"inputID",event.mp.detail)
          //console.log("当前学号：",event.mp.detail)
          this.globalData.userInfo =event.mp.detail
          console.log("当前学号：",this.globalData.userInfo)
          wx.setStorage({
                  key:"ID",
                  data:{
                    storageID:that.inputID,
                  },
                  success (res) {
                    console.log(res);
                    console.log("储存学号成功！")
                    },
                  fail (res) {
                    console.log(res)
                    //console.log("储存学号失败！")
                  }
                });
        },
      },
      
        onShow(){     
          var that=this
              Toast.loading({
              message: '加载中...',
              forbidClick: true,
                });
                
            wx.getStorage({
              key: 'Name',
              success (res) {
                that.inputName=res.data.storageName
                that.globalData.userName=that.inputName
                //console.log(res.data.storageName,that.globalData.userName)
              },
              
            })
            wx.getStorage({
              key: 'ID',
              success (res) {
                that.inputID=res.data.storageID
                that.globalData.userInfo=that.inputID
                //console.log(res.data.storageID,that.globalData.userInfo)
              },
            })

            },
            
  };


</script>

<style lang="scss" >
.wrapper {
  position: absolute;
  top: 0;
  bottom: 0;
  width: 100%;
  background-color: #f4f4f4;
}
.extra {
  background-color: #fff;
  border-radius: 10rpx;
  margin-top: 5px;
  .item {
    line-height: 1;
    padding: 25rpx 0 25rpx 20rpx;
    border-bottom: 1rpx solid #eee;
    font-size: 30rpx;
    color: #333;
  }

  button {
    text-align: left;
    background-color: #fff;
    &::after {
      border: none;
      border-radius: 0;
    }
  }
}

.right{
  text-align: right!important;
}

.icon-arrow {
  position: relative;
  &::before {
    position: absolute;
    top: 50%;
    right: 20rpx;
    transform: translateY(-50%);
  }
}
.margin{
  margin-top: 5px;
}
.profile {
  height: 375rpx;
  background-color: #3d7ef9;
  display: flex;
  justify-content: center;
  align-items: center;
  .meta {
    .avatar {
      display: block;
      width: 140rpx;
      height: 140rpx;
      border-radius: 50%;
      border: 2rpx solid #fff;
      overflow: hidden;
      margin-left: 10px;
    }
    .nickname {
      display: block;
      text-align: center;
      margin-top: 20rpx;
      font-size: 30rpx;
      color: #fff;
    }
  }
}







</style>
