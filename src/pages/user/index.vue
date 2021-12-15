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
      inputID: "",
      showModifyName: false,
      inputNewUserName: "",
      UserOldName: "",
      Password: "",
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
          account: that.UserOldName,
          password: that.Password,
          name: that.inputNewUserName,
        }),
        method: "post",
        success(res) {
          console.log(res);
          if (res.data.code == 0) {
            Toast.success("修改成功");
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
        that.UserOldName = res.data.Username;
        that.Password = res.data.Password;
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
