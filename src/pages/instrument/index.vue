<template>
  <div>
    <van-toast id="van-toast" />
    <div class="header">
      <div class="seatStatusList">
        <img class="statusLabel" src="/static/images/seat_abled.png" />
        <span>可选用</span>
        <span>&nbsp;</span>
        <img class="statusLabel" src="/static/images/slected_seat.png" />
        <span>已选中</span>
        <span>&nbsp;</span>
        <img class="statusLabel" src="/static/images/seat_used.png" />
        <span>不可选</span>
        <span>&nbsp;</span>
      </div>
    </div>

    <div class="body">
      <div class="chooseseatStatusList">
        <img
          class="statusLabel"
          @click="onClickseat('0')"
          v-show="Seatflag[0] == '0'"
          src="/static/images/seat_abled.png"
        />
        <img
          class="statusLabel"
          v-show="Seatflag[0] == '2'"
          src="/static/images/seat_used.png"
        />
        <img
          class="statusLabel"
          v-show="Seatflag[0] == '1'"
          src="/static/images/slected_seat.png"
        />
        <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>

        <img
          class="statusLabel"
          @click="onClickseat('1')"
          v-show="Seatflag[1] == '0'"
          src="/static/images/seat_abled.png"
        />
        <img
          class="statusLabel"
          v-show="Seatflag[1] == '2'"
          src="/static/images/seat_used.png"
        />
        <img
          class="statusLabel"
          v-show="Seatflag[1] == '1'"
          src="/static/images/slected_seat.png"
        />
        <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>

        <img
          class="statusLabel"
          @click="onClickseat('2')"
          v-show="Seatflag[2] == '0'"
          src="/static/images/seat_abled.png"
        />
        <img
          class="statusLabel"
          v-show="Seatflag[2] == '2'"
          src="/static/images/seat_used.png"
        />
        <img
          class="statusLabel"
          v-show="Seatflag[2] == '1'"
          src="/static/images/slected_seat.png"
        />
        <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>

        <img
          class="statusLabel"
          @click="onClickseat('3')"
          v-show="Seatflag[3] == '0'"
          src="/static/images/seat_abled.png"
        />
        <img
          class="statusLabel"
          v-show="Seatflag[3] == '2'"
          src="/static/images/seat_used.png"
        />
        <img
          class="statusLabel"
          v-show="Seatflag[3] == '1'"
          src="/static/images/slected_seat.png"
        />
        <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
      </div>

      <div class="chooseseatStatusList">
        <img
          class="statusLabel"
          @click="onClickseat('4')"
          v-show="Seatflag[4] == '0'"
          src="/static/images/seat_abled.png"
        />
        <img
          class="statusLabel"
          v-show="Seatflag[4] == '2'"
          src="/static/images/seat_used.png"
        />
        <img
          class="statusLabel"
          @click="onClickseat('4')"
          v-show="Seatflag[4] == '1'"
          src="/static/images/slected_seat.png"
        />

        <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
        <img
          class="statusLabel"
          @click="onClickseat('5')"
          v-show="Seatflag[5] == '0'"
          src="/static/images/seat_abled.png"
        />
        <img
          class="statusLabel"
          v-show="Seatflag[5] == '2'"
          src="/static/images/seat_used.png"
        />
        <img
          class="statusLabel"
          v-show="Seatflag[5] == '1'"
          src="/static/images/slected_seat.png"
        />

        <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
        <img
          class="statusLabel"
          @click="onClickseat('6')"
          v-show="Seatflag[6] == '0'"
          src="/static/images/seat_abled.png"
        />
        <img
          class="statusLabel"
          v-show="Seatflag[6] == '2'"
          src="/static/images/seat_used.png"
        />
        <img
          class="statusLabel"
          v-show="Seatflag[6] == '1'"
          src="/static/images/slected_seat.png"
        />

        <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
        <img
          class="statusLabel"
          @click="onClickseat('7')"
          v-show="Seatflag[7] == '0'"
          src="/static/images/seat_abled.png"
        />
        <img
          class="statusLabel"
          v-show="Seatflag[7] == '2'"
          src="/static/images/seat_used.png"
        />
        <img
          class="statusLabel"
          v-show="Seatflag[7] == '1'"
          src="/static/images/slected_seat.png"
        />
        <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
      </div>

      <div class="chooseseatStatusList">
        <img
          class="statusLabel"
          @click="onClickseat('8')"
          v-show="Seatflag[8] == '0'"
          src="/static/images/seat_abled.png"
        />
        <img
          class="statusLabel"
          v-show="Seatflag[8] == '2'"
          src="/static/images/seat_used.png"
        />
        <img
          class="statusLabel"
          v-show="Seatflag[8] == '1'"
          src="/static/images/slected_seat.png"
        />
        <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
        <img
          class="statusLabel"
          @click="onClickseat('9')"
          v-show="Seatflag[9] == '0'"
          src="/static/images/seat_abled.png"
        />
        <img
          class="statusLabel"
          v-show="Seatflag[9] == '2'"
          src="/static/images/seat_used.png"
        />
        <img
          class="statusLabel"
          v-show="Seatflag[9] == '1'"
          src="/static/images/slected_seat.png"
        />

        <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
        <img
          class="statusLabel"
          @click="onClickseat('10')"
          v-show="Seatflag[10] == '0'"
          src="/static/images/seat_abled.png"
        />
        <img
          class="statusLabel"
          v-show="Seatflag[10] == '2'"
          src="/static/images/seat_used.png"
        />
        <img
          class="statusLabel"
          v-show="Seatflag[10] == '1'"
          src="/static/images/slected_seat.png"
        />

        <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
        <img
          class="statusLabel"
          @click="onClickseat('11')"
          v-show="Seatflag[11] == '0'"
          src="/static/images/seat_abled.png"
        />
        <img
          class="statusLabel"
          v-show="Seatflag[11] == '2'"
          src="/static/images/seat_used.png"
        />
        <img
          class="statusLabel"
          v-show="Seatflag[11] == '1'"
          src="/static/images/slected_seat.png"
        />
        <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
      </div>

      <div class="chooseseatStatusList">
        <img
          class="statusLabel"
          @click="onClickseat('12')"
          v-show="Seatflag[12] == '0'"
          src="/static/images/seat_abled.png"
        />
        <img
          class="statusLabel"
          v-show="Seatflag[12] == '2'"
          src="/static/images/seat_used.png"
        />
        <img
          class="statusLabel"
          @click="onClickseat('12')"
          v-show="Seatflag[12] == '1'"
          src="/static/images/slected_seat.png"
        />

        <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
        <img
          class="statusLabel"
          @click="onClickseat('13')"
          v-show="Seatflag[13] == '0'"
          src="/static/images/seat_abled.png"
        />
        <img
          class="statusLabel"
          v-show="Seatflag[13] == '2'"
          src="/static/images/seat_used.png"
        />
        <img
          class="statusLabel"
          v-show="Seatflag[13] == '1'"
          src="/static/images/slected_seat.png"
        />

        <span margin-left:5px;>&nbsp;&nbsp;&nbsp;&nbsp;</span>
        <img
          class="statusLabel"
          @click="onClickseat('14')"
          v-show="Seatflag[14] == '0'"
          src="/static/images/seat_abled.png"
        />
        <img
          class="statusLabel"
          v-show="Seatflag[14] == '2'"
          src="/static/images/seat_used.png"
        />
        <img
          class="statusLabel"
          v-show="Seatflag[14] == '1'"
          src="/static/images/slected_seat.png"
        />
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
        @click="Reserve"
        >选好了<image class="btnImg" src="/static/images/run.png"></image>
      </van-button>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
import { connect } from "mqtt/dist/mqtt.js";
const date = "";
const timeSegment = "";
import Toast from "vant-weapp/dist/toast/toast";
// Toast.setDefaultOptions({ duration: 1000 });
const mqttUrl = "wxs://mqtt.emqttedu.xyz:8084/mqtt";
export default {
  data() {
    return {
      Seatflag: [
        "0",
        "0",
        "2",
        "2",
        "2",
        "2",
        "2",
        "2",
        "2",
        "2",
        "2",
        "2",
        "2",
        "2",
        "2",
      ],
      resForm: {
        account: "Xb19610115",
        password: "123456",
        reserves: {
          type: 1,
          start: 1,
          end: 1,
          devices: [1],
        },
      },
      Selectnum: "100",
      id: "0",
      userID: "",
      userName: "",
      isshow: false,
      show: false,
      Appointment: false,
      userInfo: {},
      hasUserInfo: false,
      canIUseGetUserProfile: false,
      data: "",
      avatar: "",
      imgUrls: [
        "/static/images/seat_abled.png",
        "/static/images/seat_used.png",
        "/static/images/slected_seat.png",
      ],
    };
  },
  methods: {
    onClickseat: function (id) {
      var that = this;
      //console.log(that.avatar)
      for (let index = 0; index < that.Seatflag.length; index++) {
        if (that.Seatflag[index] == "1") {
          that.$set(that.Seatflag, index, "0");
          break;
        }
      }
      if (that.Seatflag[id] == "0") {
        that.$set(that.Seatflag, id, "1");
        that.Selectnum = id;
        // console.log(that.Selectnum)
      }
      if (id == 0) {
        that.resForm.reserves.devices = [1];
      } else if (id == 1) {
        that.resForm.reserves.devices = [2];
      }
      //console.log(that.resForm.reserves);
    },
    Reserve() {
      let that = this;
      //预约
      //console.log(this.resForm);
      if (that.Selectnum == "100") {
        Toast.fail({ message: "未选中座位", duration: 1000 });
      } else {
        //console.log(this.resForm);
        wx.request({
          url: `https://ztuser.ltd/equipment_server/userReserveDevice`,
          data: JSON.stringify(this.resForm),
          method: "post",
          success(res) {
            //console.log(res);
            if (res.data.code == 0) {
              wx.switchTab({
                url: "/pages/list/main",
              });
            } else if (res.data.code == 4) {
              Toast.fail({ message: "当前时间已被预约", duration: 1000 });
            } else {
              Toast.fail({ message: "预约失败", duration: 1000 });
            }
          },
        });
      }
    },
  },

  onShow() {
    var that = this;
    // if()
    // that.Seatflag[1]=2;
    Toast.loading({
      message: "加载中...",
      forbidClick: true,
      duration: 500,
    });
    wx.getStorage({
      key: "user",
      success(res) {
        ////console.log(res);
        that.resForm.account = res.data.Username;
        that.resForm.password = res.data.Password;
        //console.log(that.resForm);
      },
      fail(res) {
        //console.log(res);
      },
    });
  },
  onLoad: function (option) {
    var that = this;
    var time = 0;
    var startTime, endTime;
    var timestamp = new Date().getTime();
    //console.log(timestamp);
    //console.log(option); //可以打印一下option看查看参数
    that.month = option.month;
    that.day = option.day;
    that.timeSegment = option.timeSegment;
    //new Date(2016,8,16,14,15,5); // 月份从0～11 所以减一
    if (option.timeSegment == 1) {
      time = 8;
    } else if (option.timeSegment == 2) {
      time = 13;
    } else if (option.timeSegment == 3) {
      time = 17;
    } else if (option.timeSegment == 4) {
      startTime = new Date().getTime();
      endTime = startTime + 10800000;
    }
    if (time != 0) {
      startTime = new Date(
        2021,
        option.month - 1,
        option.day,
        time,
        0,
        0
      ).getTime();
      endTime = new Date(
        2021,
        option.month - 1,
        option.day,
        time + 3,
        0,
        0
      ).getTime();
    }
    this.resForm.reserves.start = startTime;
    this.resForm.reserves.end = endTime;
    if (timestamp > startTime) {
      that.Seatflag[0] = 2;
      that.Seatflag[1] = 2;
    } else {
      that.Seatflag[0] = 0;
      that.Seatflag[1] = 0;
    }
  },
};
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

.statusLabel {
  margin-top: 36px;
  margin-bottom: 36px;
  width: 50px;
  height: 50px;
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
  background-color: #fff;
  border-radius: 0px 0px 10px 10px;
  border: 2rpx solid #3d7ef9;
  justify-content: space-around;
  box-shadow: #d6d6d6 0px 0px 5px;
}
.body {
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

.button1 {
  margin: 0 auto;
  width: 50%;
  position: fixed;
  bottom: 50px;
  left: 0px;
  right: 0px;
}

.data-wrapper {
  margin-top: 20px;
  display: flex;
  justify-content: space-between;
  .data {
    background-color: #fff;
    width: 150px;
    height: 80px;
    border-radius: 20px;
    display: flex;
    justify-content: space-around;
    padding: 0 8px;
    box-shadow: #d6d6d6 0px 0px 5px;
    .data-logo {
      height: 36px;
      width: 36px;
      margin-top: 15px;
    }
    .data-text {
      margin-top: 15px;
      columns: #7f7f7f;
      .data-title {
        text-align: middle;
      }
      .data-value {
        font-size: 26px;
      }
    }
  }
}
</style>
