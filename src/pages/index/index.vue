<template>
  <div>
    <div>
      <swiper
        :indicator-dots="true"
        :autoplay="true"
        :interval="5000"
        :duration="900"
        :circular="true"
      >
        <div v-for="(item, index) in imgUrls" :key="index">
          <swiper-item>
            <image :src="item" class="slide-image" />
          </swiper-item>
        </div>
      </swiper>
    </div>

    <div class="wrapper">
      <div class="button1">
        <van-button
          plain
          size="large"
          color="#3d7ef9"
          type="primary"
          @click="onClickButton1"
          >&nbsp;&nbsp;&nbsp;&nbsp;使用指南
          <image class="btnImg" src="/static/images/guide.png"></image>
        </van-button>
      </div>

      <div class="bottom-wrapper">
        <div >
          <span style="float: left">{{ City }}-{{ Area }}</span>
          <span style="float: right"
            >空气质量:{{ AirValue }}-{{ AirQualiy }}</span
          >
        </div>
        <div class="bottom-text">
          <span>{{ Weather }}:{{ Tempreal }}℃</span>
       
        </div>
        <div class="weather-advice">
          &nbsp;&nbsp;&nbsp;&nbsp;{{ WeatherAdvice }}
        </div>
      </div>
      <div class="button2">
        <van-button
          plain
          size="large"
          color="#3d7ef9"
          type="primary"
          @click="onClickButton3"
          >&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
          <span style="font-size: 16px">开始使用</span>
          <image class="btnImg" src="/static/images/use.png"></image>
        </van-button>
      </div> 
<!-- 
      <div class="button2">
        <van-button
          plain
          size="large"
          color="#3d7ef9"
          type="primary"
          @click="onClickButton2"
          >&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
          <span style="font-size: 16px">项目开发介绍</span>
          <image class="btnImg" src="/static/images/guide.png"></image>
        </van-button>
      </div> -->
    </div>
    <van-toast id="van-toast" />
  </div>
</template>


<script>
import Toast from "vant-weapp/dist/toast/toast";
// import { connect } from "mqtt/dist/mqtt.js";
// const mqttUrl = "wxs://mqtt.emqttedu.xyz:8084/mqtt";
const token = "1";

export default {
  name: "SimpleSwiper",
  props: {
    images: {
      type: Array,
    },
  },
  data() {
    return {
      client: {},
      AirValue: 20,
      AirQualiy: "请求中",
      Beep: false,
      Tempreal: 20,
      Temp: 23,
      Hum: 10,
      Light: 10,
      Led: false,
      City: "绍兴市",
      Area: "上虞区",
      Weather: "阴",
      WeatherAdvice:
        "白天有小雨，从而使空气湿度加大，会使人们感觉有点儿闷热,但早晚的天气很凉爽、舒适。",
      imgUrls: ["/static/images/swiper1.png", "/static/images/swiper2.jpg","/static/images/swiper3.jpg"],
    };
  },
  components: {},
  methods: {
    onClickButton1() {
      const url = "/pages/guide/main";
      wx.navigateTo({ url });
    },
    onClickButton2() {
      const url = "/pages/introduce/main";
      wx.navigateTo({ url });
    },
    onClickButton3() {
      const url = "/pages/time/main";
      wx.switchTab({ url });
    },
  },
  onShow() {
    var that = this;
    Toast.loading({
      message: "加载中...",
      forbidClick: true,
      duration: 500,
    });
  },
  created() {
    let app = getApp();
  },

  onLoad() {
    var that = this;
    // that.client = connect(mqttUrl);
    Toast.loading({
      message: "加载中...",
      forbidClick: true,
    });
    {
      const key = "6e8d686b843f4c2ea3b0b5e0bbc7d95b";
      wx.request({
        //天气
        url: `https://devapi.qweather.com/v7/weather/now?location=120.5802,30.03033&key=${key}`, //和风天气api地址
        success(res) {
          ////console.log(res.data)
          const { now } = res.data;
          ////console.log(now)
          that.Humreal = now.humidity;
          that.Tempreal = now.temp;
          that.Weather = now.text;
        },
      });

      wx.request({
        //生活建议
        url: `https://devapi.qweather.com/v7/indices/1d?type=0&location=120.5802,30.03033&key=${key}`, //和风天气api地址
        success(res) {
          ////console.log(res.data)
          const { daily } = res.data;
          ////console.log(daily)
          that.WeatherAdvice = daily[8].text;
        },
      });

      wx.request({
        //空气质量
        url: `https://devapi.qweather.com/v7/air/now?location=120.5802,30.03033&key=${key}`, //和风天气api地址
        success(res) {
          ////console.log(res)
          const { now, station } = res.data;
          that.AirQualiy = now.category;
          that.AirValue = now.aqi;
        },
      });
    }
  },
};
</script>
<style lang="scss"scoped>
.slide-image {
  width: 100%;
  height: 100%;
}
.btnImg {
  width: 50rpx;
  height: 50rpx;
  position: absolute;
  left: 30px;
  margin-top: 10px;
}
.button1 {
  width: 50%;
  margin: 0 auto;
  text-align: center;
  margin-top: 20px;
}
.button2 {
  width: 50%;
  margin: 0 auto;
  margin-top: 40px;
}
.wrapper {
  padding: 15px;
  .bottom-wrapper {
    background-color: #3d7ef9;
    border-radius: 20px;
    color: #fff;
    box-shadow: #d6d6d6 5px 5px 10px;
    padding: 15px 30px;
    position: fixed;
    bottom: 0;
    right: 15px;
    left: 15px;
    overflow: hidden;
    margin-top: 5px;

    text-shadow: 0px 0px 4px #000555;
    .bottom-text {
      display: block;
      font-size: 26px;
      font-weight: 150;
      text-align: left;
      margin-top: 25px;
  
    }
    .weather-advice {
      margin-top: 10px;
      font-size: 12px;
      justify-content: space-between;
      display: flex;
    }
  }
  .data-wrapper {
    margin-top: 0px;
    display: flex;
    justify-content: space-between;
    margin-bottom: 10px;
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
}
</style>
