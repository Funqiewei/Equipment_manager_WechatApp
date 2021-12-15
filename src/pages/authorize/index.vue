<template>
  <div>
    <!-- -->
    <div class="header">
      <div v-if="isLogin">
        <div class="header-title">请登录</div>
        <div class="header-info">Please Login Your Account</div>
      </div>
      <div v-else>
        <div class="header-title">请注册</div>
        <div class="header-info">Please Register Your Account</div>
      </div>
    </div>

    <div class="body">
      <div class="login-form">
        <van-field
          label="学号"
          placeholder="请输入学号"
          :value="inputUserName"
          @change="onUserNameChange"
        />
        <van-field
          label="密码"
          type="password"
          placeholder="请输入密码"
          :value="inputPassword"
          @change="onPasswordChange"
        />
      </div>

      <van-button
        type="primary"
        slot="button"
        round
        block
        color="#3d7ef9"
        border="true"
        @click="onClick"
      >
        {{ isLogin ? "登录" : "注册" }}
      </van-button>

      <div class="other-option">
        <div @click="onOptionClick">
          <span>{{ isLogin ? "注册账号" : "登陆账户" }}</span>
        </div>
        <span style="margin: 0 30px">|</span>

        <div @click="onForgetClick">
          <span password="true">忘记密码</span>
        </div>
      </div>
      <van-radio-group v-model="radio">
        <van-radio class="authorize" name="1" @click="authorize"
          >点此进行用户授权</van-radio
        >
      </van-radio-group>
      <div class="coppyright-wrapper">
        <span class="copyright">©Power By Zuoge</span>
      </div>

      <van-dialog
        use-slot
        title="找回密码"
        :show="showFindPassword"
        show-cancel-button
        @confirm="onFindPassWordConfirm"
        @cancel="onFindPassWordCancel"
        transistion="fade"
      >
        <van-field
          label="手机号"
          title-width="60px"
          placeholder="请输入绑定手机号"
          :value="inputContact"
          @change="onContactChange"
          transistion="fade"
          disable-default-padding="true"
        />
      </van-dialog>
      <van-dialog
        use-slot
        title="重置密码"
        :show="showReSetPassword"
        show-cancel-button
        @confirm="onReSetWordConfirm"
        transistion="fade"
      >
        <van-field
          label="用户名"
          title-width="60px"
          :value="inputUserName"
          readonly
        />
        <van-field
          label="新密码"
          type="password"
          title-width="60px"
          placeholder="请输入新密码"
          :value="inputPassword"
          @change="onPasswordChange"
          @cancel="onPasswordCancel"
        />
      </van-dialog>
      <van-toast id="van-toast" />
    </div>
  </div>
</template>;
<script>
import Toast from "vant-weapp/dist/toast/toast";
export default {
  data() {
    return {
      inputUserName: "",
      inputPassword: "",
      inputContact: "",
      isLogin: true,
      showFindPassword: false,
      showReSetPassword: false,
      radio: "0",
      avatar: "",
      username: "",
    };
  },
  onShow() {
    var that = this;
    wx.getStorage({
      key: "user",
      success(res) {
        wx.switchTab({
          url: "/pages/index/main",
        });
        that.radio = 1;
        //console.log(res);
      },
      fail(res) {
        //console.log(res);
      },
    });
  },

  methods: {
    authorize() {
      var that = this;
      that.radio = "1";
      wx.getUserProfile({
        desc: "用于完善设备端用户资料", // 声明获取用户个人信息后的用途，后续会展示在弹窗中，请谨慎填写
        success: (res) => {
          // //console.log(res);
          this.username = res.userInfo.nickName;
          this.avatar = res.userInfo.avatarUrl.slice(0, -3) + "46";
          ////console.log(this.name);
        },
      });
    },
    onUserNameChange(event) {
      var that = this;
      //"pages/login/main",
      that.$set(that, "inputUserName", event.mp.detail);
      //console.log("当前用户名：", event.mp.detail);
    },

    onPasswordChange(event) {
      var that = this;
      that.$set(that, "inputPassword", event.mp.detail);
      //console.log("当前密码：", event.mp.detail);
    },

    onContactChange(event) {
      var that = this;
      that.$set(that, "inputContact", event.mp.detail);
      //console.log("请输入手机号：", event.mp.detail);
    },

    onClick(event) {
      var that = this;
      Toast.loading({
        duration: 0, //持续展示轻提示
        forbidClick: true, //禁止提示时被点击
        massage: that.isLogin ? "登陆中..." : "注册中...",
      });
      ////console.log(event.mp.detail)
      setTimeout(() => {
        if (!that.isLogin) {
          //注册
          if (this.radio != "1") {
            Toast.fail({ message: "请先进行授权", duration: 1000 });
          } else {
            wx.request({
              url: `https://ztuser.ltd/equipment_server/userLogon`,
              data: JSON.stringify({
                account: that.inputUserName,
                password: that.inputPassword,
              }),
              method: "post",
              success(res) {
                //console.log(res);
                if (res.data.code == 0) {
                  wx.request({
                    url: `https://ztuser.ltd/equipment_server/userChangeImage`,
                    data: JSON.stringify({
                      account: that.inputUserName,
                      password: that.inputPassword,
                      image: that.avatar,
                    }),
                    method: "post",
                    success(res) {
                      //console.log(res);
                      // if (res.data.code == 0) {
                      // console.log("修改设备头像成功！");
                      // }
                    },
                  });
                  wx.request({
                    url: `https://ztuser.ltd/equipment_server/userChangeName`,
                    data: JSON.stringify({
                      account: that.inputUserName,
                      password: that.inputPassword,
                      name: that.username,
                    }),
                    method: "post",
                    success(res) {
                      //console.log(res);
                      if (res.data.code == 0) {
                        //console.log("修改姓名成功！");
                      }
                    },
                  });
                  //console.log("注册成功！");
                  Toast.success("注册成功");
                  that.isLogin = true;
                } else if (res.data.code == 2) {
                  Toast.fail("用户已存在");
                  console.log(res);
                } else {
                  Toast.fail("注册失败");
                }
              },
              fail(res) {
                Toast.fail("无法连接服务器");
              },
            });
          }
        } else {
          //登录
          if (this.radio != "1") {
            Toast.fail({ message: "请先进行授权", duration: 1000 });
          } else {
            ////console.log(res.data)
            wx.request({
              url: `https://ztuser.ltd/equipment_server/userLogin`,
              method: "post",
              data: JSON.stringify({
                account: that.inputUserName,
                password: that.inputPassword,
              }),
              success(res) {
                if (res.data.code == 0) {
                  console.log(res);
                  Toast.success("登陆成功");
                  wx.setStorage({
                    key: "user",
                    data: {
                      Username: that.inputUserName,
                      Password: that.inputPassword,
                      avatarUrl: that.avatar,
                      username: that.username,
                    },
                    success(res) {
                      //console.log(res);
                    },
                    fail(res) {
                      //console.log(res);
                    },
                  });
                  setTimeout(() => {
                    wx.switchTab({
                      url: "/pages/index/main",
                    });
                  }, 500);
                } else if (res.data.code == 2) {
                  Toast.fail("用户不存在");
                } else if (res.data.code == 3) {
                  Toast.fail("密码错误");
                } else {
                  Toast.fail("登陆失败");
                }
              },
              fail(res) {
                Toast.fail("无法连接服务器");
              },
            });
            // if (1) {
            //   Toast.success("登陆成功");
            //   setTimeout(() => {
            //     wx.switchTab({
            //       url: "/pages/index/main",
            //     });
            //   }, 500);
            // } else {
            //   Toast.fail("用户名/密码错误");
            // }
          }
        }
      }, 1000);
    },

    onOptionClick(event) {
      var that = this;
      that.isLogin = !that.isLogin;
      // //console.log(
      //   `切换注册/登录被点击了,当前处于${that.isLogin ? "登录" : "注册"}状态！`
      // );
    },

    onForgetClick(event) {
      var that = this;
      that.showFindPassword = !that.showFindPassword;
    },

    onFindPassWordConfirm(event) {
      var that = this;
      wx.getStorage({
        key: "user",
        success(res) {
          ////console.log(res.data)
          if (that.inputContact === res.data.Contact) {
            that.showReSetPassword = false;
            that.inputUserName = res.data.inputUserName;
            that.showReSetPassword = true;
            //console.log("找到该用户信息", res.data.Contact);
          } else {
            Toast.fail("无该用户信息");
            that.inputContact = "";
          }
        },
        fail(res) {
          ////console.log(res)
          Toast.fail("无该用户信息");
          that.inputContact = "";
        },
      });
      that.showFindPassword = !that.showFindPassword;
    },
    onReSetWordConfirm(event) {
      var that = this;
      wx.setStorage({
        key: "user",
        data: {
          Username: that.inputUserName,
          Password: that.inputPassword,
        },
        success(res) {
          //console.log(res);
          // //console.log("重置成功！");
          Toast.success("重置成功");
        },
        fail(res) {
          //console.log(res);
          // //console.log("重置失败！");
          Toast.success("重置失败");
        },
      });
    },
    onFindPassWordCancel(event) {
      var that = this;
      that.inputUserName = "";
      that.inputPassword = "";
      that.inputContact = "";
    },
    onReSetWordCancel(event) {
      var that = this;
      that.inputUserName = "";
      that.inputPassword = "";
      that.inputContact = "";
    },
  },
};
</script>

<style lang="scss"scoped>
.header {
  height: 50px;
  padding: 25px 0px;
  background-color: #3d7ef9;

  .header-title {
    font-size: 28px;
    margin-top: -10px;
    font-weight: 500;
    color: #fff;
    margin-left: 20px;
  }

  .header-info {
    font-size: 14px;
    color: #fff;
    margin-left: 20px;
  }
}
.authorize {
  position: fixed;
  margin-left: 80px;
  bottom: 80px;
}
.body {
  border-radius: 15px 15px 0 0;
  background-color: #fff;
  padding: 20px;
  .login-form {
    margin-bottom: 30px;
  }

  .other-option {
    display: flex;
    justify-content: center;
    margin-top: 20px;
    color: #9f9f9f;
  }

  .coppyright-wrapper {
    display: flex;
    font-size: 14px;
    justify-content: center;
    .copyright {
      color: #bbb9b9;
      position: fixed;
      bottom: 50px;
      margin-top: 10px;
    }
  }
}
</style>
