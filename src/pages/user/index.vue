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
          <!-- 因2022微信收回开发者在未获取用户明示同意的情况下通过 <open-data>组件 在小程序中展示用户个人信息，用户容易误以为自己的个人信息在未授权的情况下，被小程序获取。下行弃用 -->
          <!-- <open-data class="avatar" type="userAvatarUrl"></open-data> -->
          <img :src="userAvatarUrl" alt="" class="avatar">
          <!-- <text class="nickname">nickname</text> -->
          <span class="nickname">{{ showUsername }}</span>
        </div>
      </div>

      <div class="margin">
        <van-cell title="小程序版本" value="1.0.0x" />
      </div>
      <div class="margin">
        <van-cell @click="clickguide" title="使用指南" value=" " />

        <van-cell @click="clickhistory" title="当前设备信息" value=" " />

        <van-cell @click="modifyname" title="修改用户名" value=" " />
      </div>
    </div>

    <van-dialog
      use-slot
      title="修改用户名"
      :show="showModifyName"
      show-cancel-button="true"
      @cancel="onReSetNameCancel"
      @confirm="onReSetNameConfirm"
      transistion="fade"
    >
      <van-field
        label="新用户名"
        title-width="60px"
        :value="inputNewUserName"
        @change="onUserNameChange"
        placeholder="请输入新用户名"
      />
    </van-dialog>
    <van-toast id="van-toast" />
  </div>
</template>

<script>
import Toast from "vant-weapp/dist/toast/toast";
export default {
  data() {
    return {
      userAvatarUrl:"",
      inputID: "",
      showModifyName: false,
      inputNewUserName: "",
      UserName: "",
      Password: "",
      showUsername: "",
    };
  },
  methods: {
    onUserNameChange(event) {
      var that = this;
      that.$set(that, "inputNewUserName", event.mp.detail);
      console.log("新名字", that.inputNewUserName);
    },
    onReSetNameCancel() {
      var that = this;
      that.showModifyName = false;
      that.inputNewUserName = "";
    },
    onReSetNameConfirm() {
      var that = this;
      wx.request({
        url: `https://ztuser.ltd/equipment_server/userChangeName`,
        data: JSON.stringify({
          account: that.UserName,
          password: that.Password,
          name: that.inputNewUserName,
        }),
        method: "post",
        success(res) {
          console.log(res);
          if (res.data.code == 0) {
            Toast.success("修改成功");
            wx.setStorage({
              key: "name",
              data: {
                username: that.inputNewUserName,
              },
              success(res) {
                console.log(res);
                wx.request({
                  url: `https://ztuser.ltd/equipment_server/userLogin`,
                  data: JSON.stringify({
                    account: that.UserName,
                    password: that.Password,
                  }),
                  method: "post",
                  success(res) {
                    that.showUsername = res.data.name;
                  },
                  fail(res) {
                    //console.log(res);
                  },
                });
              },
              fail(res) {
                //console.log(res);
              },
            });
            wx.getStorage({
              key: "name",
              data: {
                username: that.inputNewUserName,
              },
              success(res) {
                console.log(res);
              },
              fail(res) {
                //console.log(res);
              },
            });
          } else {
            Toast.fail("修改失败");
          }
          that.showModifyName = false;
          that.inputNewUserName = "";
        },
      });
    },
    modifyname() {
      var that = this;
      that.showModifyName = true;
    },
    clickguide() {
      const url = "/pages/guide/main";
      wx.navigateTo({ url });
    },
    clickhistory() {
      const url = "/pages/list/main";
      wx.switchTab({ url });
    },
  },

  onShow() {
    var that = this;
    Toast.loading({
      message: "加载中...",
      forbidClick: true,
      duration: 250,
    });
    wx.getStorage({
      key: "user",
      success(res) {
        that.UserName = res.data.Username;
        that.Password = res.data.Password;
        let a=res.data.avatarUrl.slice(0, -2)+"0";
        that.userAvatarUrl=a;
      },
    }),
      wx.getStorage({
        key: "name",
        success(res) {
          that.showUsername = res.data.username;
        },
        fail(res) {
          //console.log(res);
        },
      });
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

.right {
  text-align: right !important;
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
.margin {
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
