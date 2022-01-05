<template>
  <div>
    <van-tabs color="#3d7ef9" :active="active" @change="onTabChange">
      <van-tab title="当前预约设备信息"> 
        <div class="info-wrapper">
          <div>
            <open-data class="avatar" type="userAvatarUrl"></open-data>
          </div>
          <div class="nickname">
            <span> 用户名:</span>{{ Username }}<br />
            <span>学号:{{ userinfo.account }}</span
            ><br />
            <span> 预约开始时间: {{ start }} </span><br />
            <span> 预约结束时间: {{ end }} </span>
          </div>
        </div>
        <div v-show="!Appointment" class="title">当前无预约设备</div>
       
        <div v-show="Appointment" class="info-wrapper">
          <div class="machine">
            <span style="left:20px"><image class="btnImg" src="/static/images/instrumentinfo.png"></image>设备信息: <br /> </span>
            <image class="btnImg" src="/static/images/instrument.png"></image><span>设备编号：{{ Cancel.device }} <br /> </span>
            <image class="btnImg" src="/static/images/open1.png" v-show="state.R!='开'"></image> 
              <image class="btnImg" src="/static/images/open2.png" v-show="state.R=='开'"></image> 
              <span>状态:{{ state.R }}<br /></span>
            <image class="btnImg" src="/static/images/voltage.png"></image><span> 电压:{{ state.U }}V<br /> </span>
            <image class="btnImg" src="/static/images/current.png"></image> <span>电流:{{ state.I }}A<br /> </span>
            <image class="btnImg" src="/static/images/power.png"></image><span>功率:{{ state.P }}W<br /> </span>
            <image class="btnImg" src="/static/images/energy.png"></image><span> 电量:{{ state.E }}kwh<br /> </span>
          </div>
          <van-button class="button" color="#3d7ef6" plain @click="cancelRes">
            取消预约
          </van-button>
        </div>
      </van-tab>
    </van-tabs>
    <van-toast id="van-toast" />
  </div>
</template>

<script>
import Toast from "vant-weapp/dist/toast/toast";
export default {
  data() {
    return {
      userinfo: {
        account: "",
        password: "",
      },
      Cancel: {
        account: "",
        password: "",
        type: "1",
        device: "",
        start: "",
        end: "",
      },
      UserControl: {
        account: "",
        password: "",
        device: "",
        Control: "",
      },
      active: "",
      describe: "启动时间:",
      Appointment: false,
      flag: 0,
      start: "无",
      end: "无",
      Username: "",
      state: {
        R: "loading",
        U: "loading",
        I: "loading",
        P: "loading",
        E: "loading",
      },
    };
  },
  created() {
    var that = this;
    setInterval(() => {
      that.current();
    }, 5000);
  },
  methods: {
    GMTToStr(time) {
      let date = new Date(time);
      let Str =
        date.getFullYear() +
        "-" +
        (date.getMonth() + 1) +
        "-" +
        date.getDate() +
        " " +
        date.getHours() +
        ":" +
        date.getMinutes() +
        ":" +
        date.getSeconds();
      return Str;
    },
    //时间戳转时间格式
    current() {
      var that = this;
      if (that.Appointment) {
        wx.request({
          url: `https://ztuser.ltd/equipment_server/userControlDevice`,
          data: JSON.stringify(that.UserControl),
          method: "post",
          success(res) {
            console.log(res);
            if (res.data.code == 0) {
              var temp = res.data.state;
              that.state.R =(temp.split("_")[0] == 0)? "关":"开";
              that.state.U = temp.split("_")[1];
              that.state.I = temp.split("_")[2];
              that.state.P = temp.split("_")[3];
              that.state.E = temp.split("_")[4];
            }
          },
          fail(res) {
            console.log(res);
          },
        });
      }
    },
    getLocalTime(nS) {
      var that = this;
      var time = new Date(parseInt(nS))
        .toLocaleString()
        .replace(/:\d{1,2}$/, " ");
      if (time.indexOf("GMT") != -1) {
        return that.GMTToStr(time);
      }
      return time;
    },
    onTabChange(event) {
      // wx.showToast({
      //   title: `切换完成`,
      // });
    },
    onChange(event) {
      var that = this;
      that.activeNames = event.mp.detail;
    },
    cancelRes() {
      var that = this;
      //console.log(that.Cancel);
      wx.request({
        url: `https://ztuser.ltd/equipment_server/userStopReserve`,
        data: JSON.stringify(that.Cancel),
        method: "post",
        success(res) {
          //console.log(res);
          if (res.data.code == 0) {
            Toast.success({ message: "取消预约成功", duration: "1000" });
            that.Appointment = false;
            that.start="无";
            that.end="无";
          } else {
            Toast.fail({ message: "取消预约失败", duration: "1000" });
          }
        },
        fail(res) {
          //console.log(res);
        },
      });
    },
    onClickButton() {
      var that = this;
      that.Appointment = false;
      this.globalData.Appointment = false;
      that.flag = 0;
      that.describe = "启动时间:";
      Toast.success("取消预约成功");
      //给后端发
    },
  },
  onShow() {
    var that = this;
    Toast.loading({
      message: "加载中...",
      forbidClick: true,
      duration: 500,
    });
    wx.getStorage({
      key: "name",
      success(res) {
         that.Username=res.data.username;
      },
      fail(res) {
        //console.log(res);
      },
    });
    wx.getStorage({
      key: "user",
      success(res) {
        that.UserControl.account = res.data.Username;
        that.UserControl.password = res.data.Password;
        that.Cancel.account = res.data.Username;
        that.Cancel.password = res.data.Password;
        that.userinfo.account = res.data.Username;
        that.userinfo.password = res.data.Password;
        //console.log(that.userinfo);
        wx.request({
          url: `https://ztuser.ltd/equipment_server/userGetReserve`,
          data: JSON.stringify(that.userinfo),
          method: "post",
          success(res) {
            //console.log(res);
            if (res.data.reserved.set.length == 0) {
              that.Appointment = false;
            } else {
              that.Appointment = true;
              that.start = that.getLocalTime(res.data.reserved.set[0].start);
              that.end = that.getLocalTime(res.data.reserved.set[0].end);
              that.Cancel.start = res.data.reserved.set[0].start;
              that.Cancel.end = res.data.reserved.set[0].end;
              if (res.data.reserved.set[0].devices[0]) {
                that.Cancel.device = "" + res.data.reserved.set[0].devices[0];
                that.UserControl.device =
                  "" + res.data.reserved.set[0].devices[0];
              }
              wx.request({
                url: `https://v1.hitokoto.cn/`,
                method: "get",
                success(res) {
                  that.UserControl.Control = res.data.hitokoto;
                },
                fail(res) {
                },
              });
            }
          },
          fail(res) {
            console.log(res);
          },
        });
      },
      fail(res) {
        console.log(res);
      },
    });
  },
};
</script>

<style lang="scss" >
.title {
  font-size: 16px;
  font-weight: 150;
  margin-top: 50px;
  margin-bottom: 10px;
  text-align: center;
}
.info-wrapper {
  margin-top: 1px;
  margin-left: 8px;
  margin-right: 5px;
  display: flex;
  // padding: 0 8px;
  overflow: hidden;
  background-color: #fff;
  box-shadow: #d6d6d6 4px 4px 8px;
}
.button {
  margin: 0 auto;
  width: 100%;
  position: fixed;
  text-align: center;
  bottom: 50px;
  left: 0px;
  right: 0px;
}
.avatar {
  float: left;
  width: 140rpx;
  height: 140rpx;
  border-radius: 50%;
  border: 1rpx solid #fff;
  overflow: auto;
  margin-top: 20px;
  margin-left: 5px;
}
.nickname {
  padding-top: 5px;
  margin-left: 12px;
  > span {
    line-height: 1.7;
  }
}
.btnImg {
  width: 50rpx;
  height: 50rpx;
  position: absolute;
  left: 70px;
  margin-top: 8px;
}
.machine {
  padding-top: 5px;
  margin-left: 15px;
  font-size: 20px;
  > span {
    margin-left: 75px;
    line-height: 2;
  }
}
</style>
